---
id: 610
title: S60待机界面原来并非不能扩展
date: 2009-02-07T22:42:24+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=610
permalink: /2009/02/07/s60-active-idle-is-3rd-party-extendable/
dsq_thread_id:
  - "250428043"
  - "250428043"
categories:
  - Development
  - Symbian
tags:
  - ECOM
  - plug-in
  - S60
  - Symbian
---
之前[在Nokia开发者论坛上看到的较为正式的解释](http://discussion.forum.nokia.com/forum/showthread.php?t=156321)是：待机（“Active Idle”或“Active Standby”）界面插件在3rd FP1及之前的版本中是无法由第三方开发的，因为它们被限制为只能从ROM中加载。就我对ECOM的了解，插件调用者确实可以通过内置的ROM Resolver限定只从ROM中加载插件，因此当时我也就相信了这些所谓的“专家答复”。

不过，今天[在ipmart论坛发现的一个软件](http://www.ipmart-forum.com/showthread.php?t=272838)使我重新开始质疑上述陈述。这个软件是一位高手从E71中提取出来的程序，引起我关注的一点是其中包含了一个“Active Idle”插件，它在我的E90上完全可以正常工作。出于好奇，我解开这个sis文件看了看，发现插件部分完全是一个标准的plug-in。也就是说它并没有采用“stub升级”，“偷换原有插件”等手段达到添加新插件的目的，而是光明正大的将自己注册为一个标准的ECOM插件。

看来Nokia开发者论坛上那些打着官腔的回复恐怕并不那么“官方”和“专业”，为了兜售其API Partner计划也不用连坑蒙拐骗的伎俩都祭出来了吧……

有空来反汇编一下，看看能不能自己写一个Active Idle的插件玩玩。