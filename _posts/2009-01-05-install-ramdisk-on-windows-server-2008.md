---
id: 566
title: 在Windows 2008下安装RamDisk
date: 2009-01-05T01:24:14+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=566
permalink: /2009/01/05/install-ramdisk-on-windows-server-2008/
dsq_thread_id:
  - "250427992"
  - "250427992"
categories:
  - Misc
tags:
  - 64bit
  - gavotte
  - RamDisk
  - Server
  - Windows2008
---
去年新买的PC配置了4G内存，虽然64bit的Windows Server 2008可以完整的访问到全部内存空间，但事实上大部分时候，仍然有相当容量的内存是处于闲置状态的，因此安装一个RamDisk来加速临时文件的存取可以更好的利用硬件资源。

RamDisk现在有很多不同的版本，虽然功能都差不多。我选择了<a target="_blank" href="https://bbs.et8.net/bbs/showthread.php?t=906641">CCF的gavotte所开发的版本</a>，免费、小巧，而且设置很方便，不像某某收费的RamDisk，还不能调整容量。

gavotte提供了64bit的版本，但如果你想安装在Windows Server 2008下，则不得不面临一个麻烦。由于微软强制要求“关键驱动”必须通过数字签名，所以安装后RamDisk后你会发现你的Windows无法启动了，它会提示“有驱动程序未通过数字签名，Windows拒绝启动”。这时你唯一的选择只能在刚启动时按F8，选择“禁用驱动程序签名强制”，从而可以顺利的进入Windows。但是，总不能每次启动时都得盯着屏幕，抓住短暂的时机抢按F8吧……

好在就有这么一个神奇的软件，可以帮你自动完成上述启动过程中的特殊步骤，完全不必人工干预，它就是<a target="_blank" href="http://citadel.x10hosting.com/readydriverplus/">“Ready Driver Plus”</a>。借助它，RamDisk终于可以在Windows Server 2008下完美使用了。虽然引入了一点安全风险，但作为Power User的你，应该不用担心这一点吧？（话说XP下没强制驱动签名不也照样裸奔嘛~）