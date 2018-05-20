---
id: 309
title: 中星微全系列摄像头的驱动程序
date: 2008-05-02T17:59:34+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=309
permalink: /2008/05/02/vimicro-camera-driver/
dsq_thread_id:
  - "262995903"
  - "262995903"
categories:
  - Software
tags:
  - camera
  - driver
  - Vimicro
  - Vista
  - Win2008
---
自从升级到Windows Server 2008 (x64)后，虽然小麻烦不断，不过基本都还顺能够克服或规避。这次要说的是摄像头，这是以前随便在小卖部买的一个“台电”摄像头，型号似乎是“MK10”。去台电网站逛了一圈，发现没有提供这款旧型号的64位驱动程序。

按照搜寻硬件驱动的惯常思维，还可以从芯片厂商入手，查了一下之前XP用的驱动程序，发现芯片是一家名为“中星微(Vimicro)”的公司生产的，遂在搜索引擎的协助下找到了它的网站。摸到下载区，发现它的驱动下载非常人性化，效仿了Creative等公司的作法，提供了自动识别芯片型号并提供驱动下载地址的工具：
  
<http://www.vimicro.com/english/product/pc003.htm>

几个简单步骤后就轻松搞定了Vista/2008(x64)下的驱动程序！

如果你尚在为摄像头找不到驱动程序而烦恼，那么不妨尝试用上面这个工具自动识别一下，说不定你的摄像头也是用的中星微的芯片哦。