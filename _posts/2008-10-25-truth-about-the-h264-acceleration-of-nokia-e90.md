---
id: 526
title: Nokia E90支持H.264视频加速的尴尬真相
date: 2008-10-25T17:43:06+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=526
permalink: /2008/10/25/truth-about-the-h264-acceleration-of-nokia-e90/
dsq_thread_id:
  - "250427958"
  - "250427958"
categories:
  - Mobile
  - Symbian
tags:
  - baseline
  - E90
  - H.264
  - N95
  - Nokia
---
在去年E90刚到手的时候，<a href="http://blog.oasisfeng.com/2007/09/06/multimedia-of-e90/" target="_blank">我曾经尝试分析过E90的视频播放硬件加速能力</a>，当时试图用内置的RealPlayer播放器播放全屏尺寸的H.264未果。后来又看到网上很多关于E90视频转换的文章，不过都没有提到过如何转换**支持内屏全尺寸播放的H.264视频**。

今天，在<a href="http://blog.oasisfeng.com/2008/10/25/release-the-power-of-cuda-in-badaboom/" target="_blank">试用Badaboom</a>之余，我又顺便深入测试了一次E90的H.264视频播放能力。经过多番对比测试，最终得出一个残酷的结论：

**<big>E90并不支持使用内置的RealPlayer播放器借助硬件加速播放内屏全尺寸(800&#215;352)的H.264视频。</big>**

<!--more-->实际的限制是视频尺寸，凡是高与宽的乘积超过76800（即320&#215;240）的H.264视频，内置的RealPlayer均拒绝播放（剩下音频部分可以正常播放）。而

[网上不少人试图说明的其它限制](http://my-symbian.com/forum/viewtopic.php?t=32623)，诸如Baseline Level、VBR、码率等大部分都是不实的。因为我用Badaboom转换了一段352&#215;198的H.264视频，选择Baseline Level 4.1、VBR、码率高达5Mbps（平均2.4Mbps），E90一样能流畅播放。

现在，结论很明显了。E90确实拥有与N95一样的视频播放加速能力，而且支持的最大分辨率完全一样，都是240&#215;320…… 多么尴尬的真相，难怪Nokia一直不推出支持E90的Video Manager了。不过话说回来，我们至少相对N95还有一点点优势，因为我们还可以享受430&#215;178的超宽银幕H.264电影，哈哈~