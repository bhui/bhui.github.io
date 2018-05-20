---
id: 1069
title: 【原创】提高专注的时间管理小工具（Win32）
date: 2012-07-21T11:01:55+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=1069
permalink: /2012/07/21/tiny-tool-for-concentration/
categories:
  - Computer
  - Development
  - Software
tags:
  - AutoHotkey
  - Time-Management
---
在被<a title="RescueTime" href="http://rescuetime.com/ref/404015" target="_blank">RescueTime</a>反复羞辱之后，痛定思痛，今天早上爬起来之后决定开发一个提高专注的小工具，拯救我的时间专注率！

其实，失去专注很多时候是由于无意识的『开小差』，或者查资料时『跑了题』，也包括来自其它插入型的干扰，比如IM消息。所以，我解决这个问题的思路很简单，也很直接：事先锁定一个窗口（比如IDE或者PowerPoint），当离开它一小段时间后，就开始闪烁任务栏的窗口标题。

实现上，用到了Win32的一个API：FlashWindow()。为了开发方便，使用了AutoHotKey作为平台，半个小时便开发调试完成。不过仅在Windows 7下测试过，如果其它版本下有问题，请反馈。

使用方法：

下载exe或者ahk（如果安装了AutoHotKey）文件，启动它之后，切换到需要专注的应用窗口，按热键『 Ctrl+Win+Alt+F 』，即可看到当前窗口在任务栏闪烁了一次，表明它已被专注。接下来只要你离开这个窗口超过1分钟，它就会开始在任务栏每分钟闪烁一遍。热键『 Shift+Ctrl+Win+Alt+F 』可以解除专注锁定。

[Concentrate.exe](http://blog.oasisfeng.com/wp-content/uploads/2012/07/Concentrate.exe) （适合普通用户）

[Concentrate.ahk](http://blog.oasisfeng.com/wp-content/uploads/2012/07/Concentrate.zip) （适合安装了AutoHotKey的用户）