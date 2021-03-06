---
id: 478
title: 微软键盘驱动与千千静听的冲突
date: 2008-10-10T23:12:45+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=478
permalink: /2008/10/10/conflict-between-microsoft-keybord-driver-and-ttplayer/
dsq_thread_id:
  - "250427875"
  - "250427875"
categories:
  - Software
tags:
  - Conflict
  - Hotkey
  - Microsoft
  - TTPlayer
---
使用微软曲线2000键盘上的多媒体快捷键控制千千静听播放音乐确实比以往的组合快捷键惬意多了。千千静听本身直接支持标准的多媒体快捷键。看到网上有人说不支持它的多媒体快捷键，我想可能有两个原因：千千静听版本不是最新（我手里的5.2版可以支持，但不清楚以往的版本是否也能）；安装了微软的键盘驱动程序，它会导致多媒体快捷键在千千静听下失效，不过微软自己的Windows Media Player不受影响。（不清楚罗技键盘的情况）

要解决后面说这个问题，要么卸载掉微软的键盘驱动，要么在使用千千静听时结束掉itype.exe这个进程。

* * *

PS：千千静听的热键设置界面中其实还可以接受多媒体热键作为新的热键，只是看不到名称的显示罢了（其实，空白不代表没有快捷键，而“无”字才是）。比如我就将“Back”和“Forward”两个快捷键分别分配给了“上一首”和“下一首”。

另外，多媒体快捷键还可以配合组合键作为千千静听的快捷键，就像我把“Ctrl+减音量”和“Ctrl+加音量”设成控制千千静听自身的音量，从而与Windows全局音量控制区分开。

* * *

**UPDATE:** 借助AutoHotkey跟踪分析了一下，发现微软驱动将键盘本身的快捷键拦截，然后再模拟发出配置的快捷键。而千千静听可能是采用的Keyboard Hook方式识别多媒体快捷键，结果因为微软的二次转换而失效。这一点还可以通过AutoHotkey的Send指令证实，因为它也无法触发千千静听的多媒体快捷键识别机制。正在研究用AutoHotkey和平解决两者冲突的可能，如有新的进展我会再更新本文。