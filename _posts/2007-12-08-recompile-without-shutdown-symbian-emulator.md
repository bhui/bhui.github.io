---
id: 291
title: VC下也能实现不重启模拟器重新编译Symbian程序
date: 2007-12-08T11:54:06+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/12/08/recompile-without-shutdown-symbian-emulator/
permalink: /2007/12/08/recompile-without-shutdown-symbian-emulator/
dsq_thread_id:
  - "255368824"
  - "255368824"
categories:
  - Development
  - Symbian
tags:
  - Code Warrior
  - Emulator
  - Symbian
  - VC
  - Visual C++
  - 模拟器
---
之前看过一些文章，在比较Symbian开发常用的两个IDE——VC和CodeWarrior时，都不约而同的提到了一点易用性上的差别：CodeWarrior不必重启模拟器就可以重新编译应用程序，言下之意用VC就必须重启模拟器才能再次编译程序并进行调试。（Carbide C++呢？老实说，我不知道，因为我一般不用那个河马一样笨重和迟缓的庞然大物……）

众所周知，Symbian模拟器的启动确实是一个漫长到可以顺便去煮咖啡的过程（机器配置高的朋友就别砸我了……），正因为上面提到的这一点劣势，很多人放弃了熟悉的VC而选择了重新学习陌生的CodeWarrior。其实，事情也不尽然如此。略施小计，我们也能在VC下实现开着模拟器重新编译应用。方法如下：

（1）在模拟器中退出你的应用程序。
  
（2）在VC下Detach EPOC进程：下拉菜单“调试”-“全部分离” 。
  
（3）OK，现在可以修改代码并重新编译你的应用程序了。
  
（4）编译好后，回到VC，重新Attach EPOC进程：下拉菜单“调试” -“进程”，在“可用进程”中选中“epoc.exe”并点击“附加&#8230;”。
  
（5）在模拟器中启动你的应用程序并继续调试吧。

上面的步骤可能稍显繁琐，但看在CW那昂贵License的份上，还是继续用我们亲切的VC吧~ 😉

注：这个方法可能不适用于调试一些特殊程序，比如OFS插件，因为它们始终在被系统使用而无法从内存中卸载。不过这种情形下我相信CW也同样没辙吧。