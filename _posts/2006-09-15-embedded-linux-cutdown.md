---
id: 101
title: 嵌入式应用Linux裁减的初次尝试
date: 2006-09-15T21:38:23+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/15/embedded-linux-cutdown/
permalink: /2006/09/15/embedded-linux-cutdown/
dsq_thread_id:
  - "250426206"
  - "250426206"
categories:
  - Development
  - Linux
tags:
  - Boot
  - BusyBox
  - Cutdown
  - Embed
  - fstab
  - initrd
  - Linux
---
　　前段时间因为嵌入式应用开发的需要，对Linux进行了一次大幅度的裁减。由于是初次接触Linux启动的核心部分，所以基本上还是对网上各种裁减方案的拼凑和整理，包含自己理解的部分实在很少。总的来说效果不算理想，后面还有很长的路要走。

这里就大致说说目前这个Linux裁减方案的“雏形”吧。

<!--more-->　　1. 内核裁减

对Linux内核部分的裁减主要根据实际需求进行了重编译，去掉了大部分用不上的特性，以及实际硬件环境之外的设备驱动。这一过程没啥技术含量，就不细说了。

2. initrd改造

常规的Linux系统启动过程中，initrd仅仅充当一个临时的rootfs，在加载实际的rootfs后即被卸载或转移。出于精简的考虑，我将原rootfs并入了initrd，让它直接充当rootfs，以节省启动时间，并减小体积。（这个改造方案相对来说最简单，也足以满足实际需要）

改造的过程主要是基于原make install自动生成的initrd镜像之上，进行以下“手术”：

(1) 用BusyBox的linuxrc替代原initrd中的初始化脚本，并将原linuxrc脚本中有用得上的初始化任务都合并至etc/inittab中，以节省启动时间。

(2) 因为要充当rootfs，所以还需为initrd添加Linux启动及运行所必须的一些文件夹和文件（主要复制自原rootfs）：

`/dev<br />
tty3 - tty10   终端会话设备（Console登录使用）<br />
ttyS0、ttyS1   串口终端设备（串口登录使用）<br />
ptmx、pts      虚拟终端设备（远程登录使用）<br />
/etc<br />
fstab          加载设备的配置文件（后面详述）<br />
gettydefs      仅保留Virtual Console一项<br />
group          仅保留root对应的项<br />
hostname       包含本机的主机名<br />
inittab        初始化脚本（后面详述）<br />
issue          包含本机的全程登录欢迎文字<br />
passwd         仅保留root对应的项<br />
shadow         仅保留root对应的项<br />
termcap        仅保留用于本地console及远程登录的配置项<br />
/etc/init.d<br />
rcS            次级初始化脚本（后面详述）<br />
/lib<br />
libcrypt.so.1  登录认证（login）所需的库文件<br />
/mnt<br />
/proc<br />
/sys<br />
/tmp<br />
/usr<br />
/var`

(3) 修改etc/fstab存储设备加载配置文件，只包含下面四行：

`sysfs /sys sysfs defaults 0 0<br />
proc /proc proc defaults 0 0<br />
tmpfs /dev/shm tmpfs size=512m 0 0<br />
devpts /dev/pts devpts defaults 0 0`

由于实际硬件环境的内存比较大，所以给临时文件系统分配的内存上限比较充裕

(4) 创建etc/inittab初始化脚本。由于init模块采用了BusyBox的精简版本，而它采用的inittab文件格式较普通版本有一些区别，所以特别按照BusyBox的格式重新编写了。文件较大，下面仅列举其中的关键部分：

`::sysinit:/bin/mount -a　加载etc/fstab中配置的所有存储设备<br />
::sysinit:/bin/mkdir /dev/shm/var　在tmpfs中划分用作var的部分<br />
::sysinit:/bin/mkdir /dev/shm/tmp　在tmpfs中划分用作tmp的部分<br />
::sysinit:/bin/chmod 1777 /dev/shm/var　修改var为合适的权限<br />
::sysinit:/bin/chmod 1777 /dev/shm/tmp　修改tmp为合适的权限<br />
::sysinit:/bin/mount --bind /dev/shm/var /var　将/var绑定到tmpfs中<br />
::sysinit:/bin/mount --bind /dev/shm/tmp /tmp　将/tmp绑定到tmpfs中</p>
<p>::sysinit:/bin/hostname -F /etc/hostname　从etc/hostname中读取并设置主机名<br />
::sysinit:/sbin/ifconfig lo 127.0.0.1 up　配置IP环回界面<br />
::sysinit:/sbin/telnetd　启动Telnet Daemon<br />
::sysinit:/etc/init.d/rcS　调用次级初始化脚本（完成不能在inittab中进行的初始化任务）</p>
<p>::sysinit:/bin/mkdir /var/log　创建日志文件夹<br />
::sysinit:/bin/touch /var/log/messages　创建日志文件<br />
::respawn:/sbin/syslogd -n -m 30 -C　加载循环缓冲模式的系统日志daemon<br />
::respawn:/sbin/klogd -n</p>
<p>::askfirst:/bin/login　在console创建登录进程<br />
tty2::askfirst:/bin/login　在tty2-tty6上创建额外的登录进程<br />
tty3::askfirst:/bin/login<br />
...<br />
ttyS0::respawn:/sbin/getty -L ttyS0 115200 vt100　在串口COM1上创建登录进程<br />
tty10::respawn:/sbin/logread -f　将所有日志打印输出到tty10`

(5) 创建etc/init.d/rcS次级初始化脚本，包含以下内容：

`/bin/mount -o remount,rw /　将rootfs重新加载为可读可写方式`

注：由于试验的方便，生成的initrd采用了Ext2文件系统。在实际应用中考虑换为CRAMFS（压缩ROM镜像文件系统），以进一步缩减镜像文件体积并提高读取效率。

3. Boot Loader修改

由于这个裁减方案仅仅使用了内核镜像及initrd，保持了与标准引导方式的高度兼容，因此适用于几乎任何Boot Loader。由于裁减实验中需要频繁替换内核和initrd镜像，因此使用了便于控制的GRUB，以提高实验效率。如果最终方案采取Flash作为镜像载体，则建议使用LILO，以提高兼容性并节省空间。
  
为了与本方案中以initrd作为rootfs保持一致，Boot Loader的配置文件中需要修改引导参数，指定“root=/dev/ram0”，无需其它额外的参数。

经过上述裁减，整个Linux的启动时间已经缩短到10s以内。内核+initrd的镜像大小也不足3M，基本达到了预期的目标。后续会针对启动的各个环节作进一步的分析和优化，以期进一步缩短启动时间。