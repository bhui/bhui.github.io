---
id: 615
title: S60第三版的Field Test也能实现锁频
date: 2009-02-08T22:53:14+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=615
permalink: /2009/02/08/lock-freq-channel-in-field-test-for-s60-3rd/
dsq_thread_id:
  - "250428144"
  - "250428144"
categories:
  - Mobile
  - Symbian
tags:
  - FTD
  - Nokia
  - S60
  - S60v3
  - Symbian
---
最早用N-Gage时，zg曾写过一个和Field Test功能相似的[NetMon](http://almalert.sourceforge.net/)，可以支持锁频，很好用。当年在峨眉山旅游时就[曾经通过锁频保证了手机上网的稳定性](http://blog.oasisfeng.com/2006/09/28/emei-tour-again/)。

此前也下载过一个S60第三版的FTD（Field Test，通信网络现场测试工具），不过一直没捣腾懂这个界面怎么用。这次升级E90固件，重新安装了[新版本的FTD](http://www.ipmart-forum.com/showthread.php?t=256986)才总算搞懂了这个玩意儿的用法。

启动FTD后，在很多页面中都能看到BTS test OFF，表示当前未开启“锁频”功能。激活锁频只需要在上述任何一页中，从菜单选择“Execute”，然后输入频段号即可。当前的频段号在第一页中的FreqCh栏里显示着。输入3333即可关闭锁频，回到正常状态。

小技巧：切换到0（或者其它任何无信号的频段）即可达到当年葛优在《手机》中开机强行拔电池的效果——“暂时无法接通”（或者“不在服务区”）。;)