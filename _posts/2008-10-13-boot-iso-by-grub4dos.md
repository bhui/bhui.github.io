---
id: 496
title: 借助GRUB4DOS在U盘上引导ISO镜像
date: 2008-10-13T23:33:09+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=496
permalink: /2008/10/13/boot-iso-by-grub4dos/
dsq_thread_id:
  - "250427892"
  - "250427892"
categories:
  - Computer
  - Linux
tags:
  - Boot
  - CD-ROM
  - Vista
  - Windows2008
---
根据cch在上一篇[《新电脑的规格配置》](http://blog.oasisfeng.com/2008/10/13/my-new-pc/)一文中的留言提示，我下载了Hitachi Feature Tool工具，打算将我的WD640AAKS也调节为高性能模式。不过面临的直接问题是这个工具是以ISO格式的光盘镜像提供，其中封装的是IBM DOS和FTOOL工具。而我没有刻录光驱，也无法安装DOS系统（全部分区都被我格式化为NTFS了），想要引导这个镜像还真有点麻烦。

正好一直以来都想解决U盘引导多重ISO镜像的难题，于是便去网上找答案，最后让我发现了GRUB4DOS这个非常强大的系统引导辅助工具。它的文档写的很详细，覆盖了各种场景下的安装方法。即使像我这样从未玩过Vista/Win2008中BCD引导系统的新手，也能按部就班的顺利装上GRUB4DOS。其实步骤说起来也很简单：（仅适用于Vista/Win2008）

<!--more-->首先应将你的U盘分区转换为可引导分区：（注意将“U:”换成实际U盘的盘符）

<pre>bootsect /nt60 U: /force /mbr</pre>

接下来需要借用Vista/Win2008安装介质中的引导部分，将其中的bootmgr、bootmgr.efi以及整个boot和efi文件夹复制到U盘上（根文件夹下）。

（因为我手中这个优盘之前就做成了Win2008的安装盘，因此省去了上面两步）

然后需要修改BCD记录，为GRUB4DOS增加引导项：

<pre>bcdedit /store U:bootbcd /create /d "More..." /application bootsector</pre>

正常情况下，你会得到一个形如“{05d33150-3fde-11dc-a457-00021cf82fb0}成功创建”的提示。这个“{&#8230;}”就是新引导项的ID，将要用在下面的几条命令中（注意将{id}替换为上述提示中的“{&#8230;}”)：

<pre>bcdedit /store U:bootbcd /set {id} device boot
bcdedit /store U:bootbcd /set {id} path grldr.mbr
bcdedit /store U:bootbcd /displayorder {id} /addlast</pre>

然后将grldr.mbr、grldr和menu.lst复制到U盘的根文件夹下即可。

接下来要修改menu.lst，增加对光盘的引导选项。编辑menu.lst文件，在第一个“title”所在行之前插入如下内容：

<pre>title Hitachi Feature Tool
map --mem (hd0,0)/ftool.iso (hd32)
map --hook
chainloader (hd32)
savedefault --wait=2</pre>

因为这个光盘镜像其实很小，所以我使用了&#8211;mem参数将其缓存到内存中。对于较大的ISO文件，最好去掉&#8211;mem参数。（除非你的内存足够容纳下）

最后包含“savedefault”那行不是必须的，它只是让你可以在引导时将这个项保存为默认值。

完成上述步骤后，再把光盘镜像文件ftool.iso丢到和grub同样的根文件夹下就完工了。

重新启动后，在Vista的启动选单中选择“More&#8230;”，然后就会出现GRUB的引导菜单，其中第一项就是我们希望引导的光盘镜像了。

GRUB4DOS强大的功能远不止引导光盘镜像、WinXP、Win9x、DOS、Linux、Mac OS全都不在话下，而GRUB4DOS本身也支持多种加载方式：MBR、boot.ini、BCD、PXE…… 以后有时间再来细细研究了，反正目前主要是用它来在U盘上多重引导ISO镜像。

* * *

倘若引导不成功，通常可能的原因有：

（1）光盘镜像的CD-ROM文件系统是Joliet CD格式，GRUB4DOS不支持这种格式。你需要通过工具转换一下镜像文件的文件系统格式。
  
（2）BIOS中激活了SATA的AHCI模式。GRUB4DOS可能无法兼容AHCI模式，应在BIOS中将SATA模式设置为IDE。

* * *

**UPDATE:** 倘若不需要兼做Vista/Win2008的安装U盘，那么完全可以删除掉bootfonts下多余的繁体中文、日文、韩文等字体文件，可以节省不少空间。bootmgr.efi及整个efi文件夹按理也可以删掉，只要用起来没有兼容性问题。