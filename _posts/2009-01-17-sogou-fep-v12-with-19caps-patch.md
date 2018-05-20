---
id: 599
title: 搜狗手机拼音1.2版，不错！（附19权限补丁）
date: 2009-01-17T15:21:41+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=599
permalink: /2009/01/17/sogou-fep-v12-with-19caps-patch/
dsq_thread_id:
  - "250428071"
  - "250428071"
categories:
  - Symbian
tags:
  - 19caps
  - fep
  - ime
  - sogou
  - Symbian
---
让我毫不犹豫的选择搜狗拼音作为手机输入法的原因很简单，<del datetime="2009-02-22T13:45:03+00:00">它是目前唯一完美支持E90内外屏的拼音输入法</del>。**[Update: 搜狗输入法于去年9月2日在网上泄露的内测版本可以看作是第一个无缝支持E90双键盘的S60输入法，其后点讯和A4均相继推出了支持E90双键盘的版本]**

1.2版本的改进相当大：

  * 终于加入了缺失已久的智能英文输入方式，算得上一个完整的手机输入法了！
  * 在线词库备份是意料之中的新特性，虽然还没有实现与PC版本词库的同步，但已经是一个很大的进步了。下一步估计会上手机版专用的细胞词库了吧。（考虑到性能的巨大差异，手机与PC同步词库可能还有一段路要走）
  * 通讯录词库的导入及针对特定程序的默认输入状态优化充分体现了以人为本的设计理念，在细微之处让你舒心。不过我试了之后发现，这个版本导入的通讯录词库似乎并不完整，有些人名还是没有。

<!--more-->BTW，数字键/全键盘免摇杆的设置对E90的支持比较有意思，开合盖时分别可以进入各自状态的设置，而不能进入与状态不对应的设置。看来搜狗手机拼音的开发团队对Symbian SDK接口的理解上比较到位。

虽然有不少网友提到内存占用增长了很多，但对于E90来说是没啥感觉的。:)

有点开始喜欢上现在这个锐意进取的搜狗了！用脚投票，谷歌拼音闪一边去吧。

* * *

**19权限修改方法**</p> 

用S60v3 SDK中的elftran对c:sysbin中的sogoufep.dll进行如下修改：

`elftran -capability "CommDD+PowerMg<br />
mt+MultimediaDD+ReadDeviceData+WriteDeviceData+TrustedUI+ProtServ+DiskAdmin+Netw<br />
orkControl+SwEvent+NetworkServices+LocalServices+ReadUserData+WriteUserData+Loca<br />
tion+SurroundingsDD+UserEnvironment+AllFiles+DRM" sogoufep.dll`

附上一个修改好的文件，供没有安装SDK的朋友使用：[sogoufep.dll](http://blog.oasisfeng.com/wp-content/uploads/2009/01/sogoufep.dll)