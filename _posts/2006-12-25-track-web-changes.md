---
id: 181
title: 跟踪网络变化，信息尽在掌握
date: 2006-12-25T00:25:16+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/12/25/track-web-changes/
permalink: /2006/12/25/track-web-changes/
dsq_thread_id:
  - "250426745"
  - "250426745"
categories:
  - Internet
tags:
  - Internet
  - NetMind
  - TrackEngine
  - WatchThatPage
  - Web
---
　　今天收到TrackEngine的通知邮件，前段时间我在0day寻觅已久的一款软件终于有了Release。兴奋之余，才发觉其实我的网络生活还是离不开“NetMind”。

　　话说自“NetMind”关闭之后，我就一直难以找到一个合适的替代品，直到此前因为在0day找寻一个软件未果，才真正想到去探索一下类“NetMind”的在线服务。经过一段时间的试用，发现有两个网站比较令我满意：

<!--more-->（1）

<http://www.watchthatpage.com>
  
　　免费（赞助可获得优先跟踪），不限制跟踪的网页数量。也正是因为这两个原因，WatchThatPage的跟踪时效性显得稍差。另外，其关键字匹配只能按照Channel设定，这一点实在有些不太人性化。

（2）<http://www.trackengine.com>
  
　　免费/收费，免费用户只能跟踪5个页面（也太小气了点……），其关键字匹配功能非常强大，段落识别较为准确！另外，支持Cookie也是它的一大优势！

　　大部分的跟踪需求，我一般选择WatchThatPage，除了部分识别有误或者特殊跟踪需求的网页才使用TrackEngine（毕竟只有5个名额）。

附：提供一个WatchThatPage的Bookmark Button URL: 

`javascript:void(open('http://www.watchthatpage.com/checkExtern.jsp?email=<strong>你的Email地址</strong>&url='+escape(location.href), 'WatchThatPage', 'height=400, width=600, location=no, scrollbars=yes, menubar=no, toolbar=no, directories=no, resizable=yes'));`

（记得将“你的Email地址”替换为注册的Email）

BTW：为什么Firefox不能正确将URL中的%2B转换为“+”？我用[以前提到的含“+”的Email地址](http://blog.oasisfeng.com/2006/11/11/use-gmail-to-track-junk-mail/)嵌入URL总是不成功，还望高手赐教！