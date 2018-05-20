---
id: 276
title: Mouse Gestures Plus!
date: 2007-10-24T01:44:28+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/10/24/mouse-gestures-plus/
permalink: /2007/10/24/mouse-gestures-plus/
dsq_thread_id:
  - "255392016"
  - "255392016"
categories:
  - Development
  - Software
tags:
  - AutoHotkey
  - mouse
---
Deguix的&#8221;Mouse Gestures&#8221;脚本将<a href="http://www.autohotkey.com/" target="_blank">AutoHotKey</a>的应用提升到了一个崭新的高度，使其远远超越了[“热键”本身所涵盖的范畴](http://blog.oasisfeng.com/2007/01/19/from-hoekey-to-autohotkey/)。这两天抽空看了一下它的代码，感觉算法还是不错，可扩充性的设计也比较灵活。通过将用户扩充指令写入脚本，然后调用AutoHotKey执行之，实现了近乎无限可能的手势指令。可惜这种理想化的可扩充性设计带来了一个很严重的后果——明显的性能降低。实际使用中发现，手势划完松开鼠标右键后，大约有半秒到1秒的延迟才能触发动作，这在开了较多程序后更为明显。（我这三年前的老机……）

今天将原脚本优化了一下，解决了性能瓶颈，并修正了一些小bug：

<!--more-->·引入预加载的指令脚本，大幅度提升了手势指令的执行速度，并可实现原有机制无法实现的“关联动作”（如最小化和恢复上一个最小化窗口）及“重新载入”等功能。


  
使用方法：在Actions.ahk中增加手势对应的标签（手势名+Action）和代码即可，代码末尾别忘了Return。
  
·去掉了几处不必要的文件读写操作，提高了性能。
  
·改为仅用右Ctrl键切换启用和禁用，避免无意识的禁用。
  
·修正了划手势过程中占用CPU过高的问题。
  
·优化了手势识别算法，提升了识别的快慢适应性和距离灵活性。
  
·增加了对可折返手势的支持，例如“右-左-右-左”。
  
·增加了已识别手势及所出发相应动作的气泡提示。
  
·增加了“防止误划手势”的功能，以忽略小幅度的右键拖拽（通过SensitivityDistance调节阈值）。
  
·调整了还原右键点击的实现，去掉了效果不理想的“分坐标按下和松开”。
  
·优化了配置文件格式，去掉了一些冗余部分，并增强了可读性和易修改性。
  
·缩短了指示色彩图标的持续时间。

考虑到原作者的“Mouse Gestures”已经很久未更新了，目前打算以“Mouse Gestures Plus!” 的名义发布并更新版本，欢迎大家试用和反馈问题！

[Download &#8220;Mouse Gestures Plus! v1.0&#8221;](http://blog.oasisfeng.com/wp-content/uploads/2007/10/mouse-gestures-plus.rar "Mouse Gestures Plus!")（需要首先安装<a href="http://www.autohotkey.com/" target="_blank">AutoHotKey</a>）