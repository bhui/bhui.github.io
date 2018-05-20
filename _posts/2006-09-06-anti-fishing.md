---
id: 94
title: 又遇Fishing Email
date: 2006-09-06T02:41:46+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/06/anti-fishing/
permalink: /2006/09/06/anti-fishing/
dsq_thread_id:
  - "250426187"
  - "250426187"
categories:
  - Internet
tags:
  - Computer
  - Internet
---
　　虽然这次的Fishing Email技术含量并不高，但屡次遭遇这种高危的欺诈行为，实在觉得有必要提醒一下各位朋友。

　　这里就我个人的认知范畴谈一下Fishing Email/Site中最常见的欺诈手段——“链接伪装”及背后可能用到的各种技术：（仅以IE为例）

<!--more-->　　（1）千万别相信“下划线上面的URL”，实际的链接可能与字面并不一样。这是最初级的欺诈手段，比如

[http://www.paypal.com/](http://blog.oasisfeng.com/)并不是指向PayPal；

　　（2）千万别相信“浏览器状态栏的URL”。这是稍微进阶一点的欺诈手段，需要一点script技巧，比如<a onmousemove="window.status='http://www.paypal.com';" onmouseover="window.status='http://www.paypal.com';" onmouseout="window.status='';" href="http://blog.oasisfeng.com/">http://www.paypal.com/</a>，鼠标移到上面时浏览器状态栏显示的还是PayPal？实际点一下试试呢？

　　（3）别以为你看了链接属性就可以放心了。这一招能防范上述两种欺诈手段，但你可能就落入了另一个圈套，比如<a href="http://www.paypal.com/" onclick="window.location.href='http://blog.oasisfeng.com/'; return false;">http://www.paypal.com/</a>（直接点击），常常让人防不胜防。

　　读到这里，或许有些朋友就要开始拍砖了，“链接再阴险，点进去之后一看地址栏不就真相大白了？”话虽如此，不过你确定你有辨别URL真伪的能力？不妨试试下面的链接：

　　打开之前，先猜猜它会带你到哪一个网站？
  
　　a. 我的Blog　b. PayPal　c. Google

http://www.paypal.com∕cgi-bin∕login.php&session\_uid=DQU\_v\_tD5ZeV\_CaTc@1089060200/search?&q=MOctOdGnEfSIsAotodGoLB

　　谈了这么多欺诈手段，那到底什么样的链接才是安全的呢？还是**自己输入网址进去**的网站才是安全的，为防万一，大家最好不要轻易用鼠标点击存在欺诈可能的链接。

　　注：上述网址纯属杜撰，仅供技术研究和学习，请勿用于其它用途。