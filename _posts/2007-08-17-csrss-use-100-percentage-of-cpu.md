---
id: 260
title: '脆弱的Windows——又遇csrss.exe 100%CPU占用问题'
date: 2007-08-17T21:54:36+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/08/17/csrss-use-100-percentage-of-cpu/
permalink: /2007/08/17/csrss-use-100-percentage-of-cpu/
dsq_thread_id:
  - "250427455"
  - "250427455"
categories:
  - Software
tags:
  - '100%'
  - ATI
  - CPU
  - csrss
  - mouse
  - Windows
  - WinXP
  - 右键
  - 驱动
  - 鼠标
---
今天开机后突然发现鼠标右键菜单弹出速度变得奇慢无比，并伴随着短时间内系统呈假死状…… 打开任务管理器一看，原来是鼠标右键菜单弹出期间csrss.exe占用了大量CPU。

遇到这种问题，直觉首先是警惕病毒/木马的侵袭，但经过多方扫描，基本排除了这种可能。不过这年头动不动就占用100%CPU的垃圾木马也能肆虐互联网，可见编程技术的江河日下…… 因为之前什么Explorer、svchost占用100%CPU的问题遇的多了，大部分时候还是出在Windows本身与安装的应用程序兼容性上，虽然还是第一次遇到csrss.exe出此症状，但也可能性颇大。搜索了一下互联网，解决方法大多是向你推荐某某杀毒软件，好不容易找到几个非病毒原因的案例却也是药不对症。偶然间找到了一篇微软支持中心的文章<a href="http://support.microsoft.com/?scid=kb%3Ben-us%3B555021&x=12&y=13" target="_blank">《Csrss.exe uses 100% of the CPU When you Right-Click an item in Explorer》</a>，提到在Explorer或桌面点击鼠标右键时出现csrss.exe占用100%CPU的症状，原因可能是用户帐号配置信息损坏。但解决措施却吓了我一跳：**直接删除并重新创建用户帐号配置信息。**这么轻描淡写的几句话，要不是对Windows稍有了解的用户，恐怕会举手之间就已造成无法挽回的损失了。

考虑再三，又经仔细推敲，发现我所遇症状其实还略有差别。不仅Explorer和桌面会出现这个症状，就连随处点击鼠标右键的标准弹出菜单都是一般。于是，我还是暂时放弃尝试上面的“解决之道”，选择继续探索答案。无意中发现一位网友提到在“显示属性-外观-效果”中关闭“淡入淡出”的菜单弹出效果可解决此问题，初见之下，颇不以为然。想Windows XP成名数载，又修炼了无数补丁，岂会因这么简单一个问题而导致内息不畅，经脉错乱。没想到一试之下竟然立即奏效！不仅概叹WinXP之脆弱，实不亚于系出同门的兄弟IE。

回想起来，昨晚睡觉前安装了ATI的最新催化剂驱动7.8版本 ，多半才是真正的罪魁祸首。可怜我的9550虽尚能饭，却早已被AMD/ATI的驱动开发团队给遗忘了……