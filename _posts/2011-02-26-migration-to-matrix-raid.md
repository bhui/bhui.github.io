---
id: 995
title: 从单硬盘向Intel Matrix RAID的无损迁移
date: 2011-02-26T21:32:10+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=995
permalink: /2011/02/26/migration-to-matrix-raid/
dsq_thread_id:
  - "250429990"
  - "250429990"
categories:
  - Computer
tags:
  - ASUS
  - Intel
  - Matrix RAID
  - RAID
  - RST
---
趁这次为女友升级电脑，顺便给自己的PC作了一次廉价的升级：将E8400 CPU超频了40%，再添置了一块硬盘组建Matrix-RAID（其中少量空间部署RAID-1，用于保存照片、文档等重要文件；其余空间全部部署RAID-0，以提升电脑性能。），总共只花费了不到￥300。

当初在购置这台主机时，曾经深入考察了Intel Matrix RAID技术（现改名为Rapid Storage Technology），其“无损迁移RAID”机制成了吸引我购买ICH10R主板的关键动力之一。两年半后，终于有机会开始利用这个技术升级现有的电脑时，我却发现这其中所深藏的玄关，远没有当初想象的那么简单……

<!--more-->　　首先，Intel在手册中声明，使用“RAID无损迁移”的前提是现有系统满足“RAID-Ready 条件”：

  * System with a supported Intel chipset
  * One Serial ATA (SATA) hard drive
  * RAID controller enabled in the BIOS
  * Motherboard BIOS that includes the Intel® Rapid Storage Technology option ROM
  * Intel® Rapid Storage Technology software
  * A partition that does not take up all of the space on the hard drive (4-5MB of free space should be sufficient)

这个条件倘若不细看，倒不会觉得有啥门槛。但其实大部分用户（包括我）都会在安装Windows时忽视其中的第三条，因为主板的BIOS配置中一般都默认关闭了RAID控制器，而我们通常不会无端的为没有RAID配置的系统开启RAID控制器。所以，当你后来买了一块新硬盘，打算升级到RAID时，才会发现这是一件多么悲剧的事情……

我首先做的是，想当然的在BIOS中激活RAID控制器。但马上你就会发现，Windows无法启动了。在网上查了一下资料，原来Windows必须在启动的早期环节加载RAID控制器的驱动程序，才能在RAID环境下正常启动。可是如何才能为一个最初安装时并没有激活RAID的Windows系统安装RAID控制器驱动呢？安装驱动程序的前提是硬件存在且没有在BIOS配置中禁用，而激活RAID控制器却又会导致Windows本身无法启动，这似乎构成了一个无解的矛盾……

在被这个问题困扰了许久之后，我无意中在翻看主板说明书时，发现了华硕P5Q主板上一个已经被完全遗忘的功能：附加的Marvel SATA控制器。华硕P5Q通过这个额外的SATA控制器提供多达8个SATA设备（显然对于家用电脑来说，绝对是一个噱头……），而宣传的“Drive Xpert”功能对于一个高级用户来说又显得毫无意义，所以这个SATA控制器一直被我打入冷宫，长期禁用掉了。但这一次，它却带给我一闪的灵光，终于让我想到了一个化解上述矛盾的办法：

  1. 先将硬盘数据线从Intel南桥的SATA口上取下来，插入Marvel控制器的SATA口。
  2. 然后打开电脑，进入BIOS配置，启用Marvel SATA控制器（如果此前禁用了）及南桥的的RAID控制器。
  3. 接下来进入Windows（因为硬盘接在Marvel的SATA口上，仍然工作在非RAID模式下，所以Windows得以正常启动），会自动识别到激活的RAID控制器。
  4. 安装Intel的Rapid Storage Technology驱动程序和管理工具，在提示重启时选择“稍后重启”。
  5. 关闭电脑，将硬盘数据线接回南桥的SATA口。
  6. 再次启动电脑，进入Windows（因为刚才已经为Intel RAID控制器安装了驱动程序，所以现在Windows不会无法启动了）。

自此，你的系统就从“非RAID”变为Matrix RAID迁移所要求的“RAID-Ready”状态了。现在可以接上新硬盘，开始用RST管理程序开始向Matrix RAID无损迁移了~

* * *

总结：让Windows从“非RAID配置”成功转变为RAID-Ready的关键在于既能让Windows正常启动，又可以识别到Intel的RAID控制器。在我的案例里，借助华硕P5Q主板所额外集成的Marvel SATA控制器做到了这一点。而对于大部分普通主板用户而言，或许有以下几种办法：

  * 激活RAID控制器，用安全模式启动，安装Intel RST驱动。（抱歉，我本应试验一下这个方法的可行性，可惜是在后来才想到的）
  * 去淘或者借一个廉价的二手SATA接口卡，临时用来起到我前面所说Marvel SATA控制器的作用
  * 取下原硬盘，接上新硬盘，激活RAID控制器，然后新安装一个Windows（安装过程中可能会提示你插入带RAID驱动程序的软盘或U盘）。安装完成后再接上原硬盘，复制数据到新硬盘后，清除原硬盘的分区并作为RTS无损迁移时的“新硬盘”。这个办法相当费时，但至少除了重装Windows之外实现了数据的无损。