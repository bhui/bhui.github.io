---
id: 459
title: 让Dropbox同步任意位置的文件
date: 2008-10-05T15:41:34+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=459
permalink: /2008/10/05/sync-files-anywhere-by-dropbox/
dsq_thread_id:
  - "250427858"
  - "250427858"
categories:
  - Computer
  - Internet
tags:
  - Dropbox
  - NTFS
  - synchronize
---
最近因为需要在办公室和家里两地同步文件，开始寻觅合适的解决方案，在网上摸索了一阵子，发现了<a href="http://www.getdropbox.com/" target="_blank">Dropbox</a>。这个软件的设计思路确实不错，实时监视My Dropbox文件夹中的变化并自动同步到服务器或从服务器同步。由于同步过程是异步进行的，因此避免了映射型网络存储访问时的高延迟。但遗憾的是，它要求必须将需同步的文件放置在预定义的My Dropbox文件夹下，这就大大制约了其应用范围，充其量只能当做一个网络U盘使用了。

我希望的是一个可以指定任意位置的文件进行同步的工具，而且需同步的文件在各同步终端上可能存放于不同的位置。比如我需要同步FlashFXP的站点配置文件sites.dat，并且我在家里将FlashFXP安装在D:ProgramsFlashFXP中，而在公司的安装位置是C:Program FilesFlashFXP。到Dropbox的官方论坛兜了一圈，发现这个特性尚在Medium Term Plan中。没办法，只好先自己动手解决这个问题。

<!--more-->首先尝试在My Dropbox下创建一个指向需同步文件的符号链接(Vista/Win2008的NTFS新增特性，使用命令mklink)，看起来Dropbox确实正确同步了该符号链接的源头，并传到了服务器上。不过在识别更新上出现了问题，无论实际文件如何变化，Dropbox都不会进行同步。估计是因为符号链接的日期不会随实际文件而更新的缘故吧。这条路看来是走不通了……

软的不吃来硬的，在My Dropbox下创建一个NTFS的“硬链接(Hard Link)”（使用命令mklink -h），结果仍然面临与符号链接相同的识别更新问题。虽然硬链接在表现上看起来与正常文件完全一致，但当你从一处修改了文件后，其它硬链接的文件描述信息（例如文件尺寸、修改日期）并未更新，除非你再次打开硬链接（即使并不改写）。引用MSDN上的一句原话：

> [However, directory entries for hard links are updated only when a user accesses a file by using the hard link.](http://technet.microsoft.com/en-us/library/cc781134.aspx)

再试了“文件夹联接(Junction)”，结果依旧…… 真是无语了，没想到NTFS进过几代的变革，依然这么落后，比起Linux/Unix的实现差远了啊。

看来，只能上土办法了。用<a href="http://dimio.altervista.org/eng/" target="_blank">DSynchronize</a>这个小工具自己定义了一个实时同步规则，从FlashFXP的程序文件夹中将sites.dat同步到My Dropbox。这样，总算糅合了两个工具，实现了我的两地同步需求。

最后，值得一提的是DSynchronize这个小工具，之所以用它来做实时同步，不仅因为它支持以系统服务方式于后台运行，还具有很多与我的软件选择价值观相符的特征：无需安装、体积小巧（不足200k）、节省资源（低于3M内存）、界面朴实、无冗余功能。唯一的遗憾是，它的实时同步竟然是通过每隔5s的文件夹轮询实现的，对于层次较深的文件夹可能会有性能负担。