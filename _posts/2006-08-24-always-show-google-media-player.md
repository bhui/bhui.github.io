---
id: 19
title: Always show Google Media Player
date: 2006-08-24T13:22:00+00:00
author: oasisfeng
layout: post
guid: http://www.oasisfeng.com/blog/2006/08/24/always-show-google-media-player/
permalink: /2006/08/24/always-show-google-media-player/
dsq_thread_id:
  - "250426020"
  - "250426020"
categories:
  - Development
  - Internet
tags:
  - Google
---
　　最近Gmail为大家提供了在线版的MP3附件播放器，据[8个圈圈网友的分析](http://bloooooooogger.blogspot.com/2006/08/gmailmp3.html)，其实它调用的正是Google Video所内嵌的媒体播放器，不光能播放MP3，还能播放其它视频。下图是Google Media Player没有加载文件时的原型，可以清楚的看出它的真面目来：

**Google Media Player**

<embed src="https://mail.google.com/mail/html/audio.swf" style="width: 400px; height: 27px;">
</embed>　　但如果想要引用这个播放器作潜入Blog中或用于其它地方时，你就会发现一个离奇的现象：凡是Google自己host的媒体文件，出现的是Flash版的播放器；但用于Google之外其它地方的媒体文件时，却成了Media Player&（FireFox的用户不会出现这一情况），如下图：

**芝华士广告歌 (Hosted by Google)**

<embed src="https://mail.google.com/mail/html/audio.swf?audioUrl=https://meteorfalling.googlepages.com/mp3" style="width: 400px; height: 27px;">
</embed>

**莫文蔚 &#8211; 如果没有你 (Hosted elsewhere)**

<embed src="https://mail.google.com/mail/html/audio.swf?audioUrl=https://blog.oasisfeng.com/wp-content/uploads/2006/09/24hrs.mp3" style="width: 400px; height: 27px;">
</embed>　　经过仔细的跟踪分析，发现原来Google在其中作了一点小小的手脚，它会首先判断媒体文件的URL，如果不是自己网站的文件且浏览器是IE，则加载Windows默认的Embed实现，也就是WindowsMediaPlayer（其实Flash播放器只是躲起来，并非不可用）。

　　那么能否让Google Media Player对所有文件一视同仁呢？呵呵，答案是显然的。我们只需对它略加修改即可达到这个目的。（**警告：此修改仅限于学习和研究目的，请勿使用在其它场合，否则后果自负！**）

　　修改的代码我就不列出来了，大家自己查看源文件吧。

**莫文蔚 &#8211; 如果没有你 (Hosted elsewhere)**