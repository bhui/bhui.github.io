---
id: 524
title: 释放CUDA的威力——Badaboom视频转换试用手记
date: 2008-10-25T16:08:21+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=524
permalink: /2008/10/25/release-the-power-of-cuda-in-badaboom/
dsq_thread_id:
  - "250427918"
  - "250427918"
categories:
  - Computer
  - Software
tags:
  - Badaboom
  - CUDA
  - H.264
  - HDTV
  - nVidia
---
忍痛割舍了过去长期钟爱的ATI，[选择了nVidia显卡](http://blog.oasisfeng.com/2008/10/13/my-new-pc/)，不是因为PhysX技术带来的游戏效能，而是看中了在非游戏应用中前景广阔的CUDA！

作为展示CUDA在非游戏领域实用价值的代表作，[Badaboom](http://www.badaboomit.com/)以惊人的视频转换速度，被各大媒体广为传颂。对于这样一款富有传奇色彩的软件，我自然要亲自品鉴一番了。

Badaboom在前不久刚刚发布了正式的1.0版本，相比此前Beta4实在看不出有什么改进。**支持的输入视频格式仍然很少，不支持最流行的mkv封装格式和Xvid视频编码是Badaboom最大的硬伤。**好在借助[tsMuxeR](http://forum.doom9.org/showthread.php?t=134104)转换一下封装格式（mkv -> ts）倒也能让Badaboom接受大部分H.264的视频。

<!--more-->转换速度确实没的说，让PMP设备的视频格式转换这一步不再是难以承受的负担！用我的9600GSO转换720p的HDRip H.264电影，在默认频率（550/1600）下也能达到100fps以上的速度，超频（750/2000）后，可达到接近150fps！转换整部4G左右的HDRip影片推算下来只需20分钟左右。

CPU占用率只有大约35%，偶尔会飙升到50%左右，不过从实际感受上，基本不影响常规的电脑使用。这一点绝对意义重大，因为你不必再被迫把电脑的使用权让给视频转换软件（我想没人愿意忍受一边转换视频一边龟速的使用电脑吧……？），而它只需使用在你上网或处理一般事物时基本“闲置”的GPU资源即可完成任务。

说了这么多激动人心的，下面要开始批评几句了。对于H.264编码的输入，转出的视频间歇性的出现莫名其妙的“抽筋”（画面前后帧来回剧烈抖动），严重影响观看。试了好几个片源都一样，而MPEG2则没有问题。音画不同步基本上是必然出现的，好在不同步的时长似乎不会随时间变化。转换某些MPEG2视频时会崩溃，比如我手中这个CHD版本的《独立日》(Independence.Day.h264-to-mpeg2.1080P.oar.dts)。输出的分辨率只有几档可选，无法自行设定……

说实话，这种粗糙的软件质量就发布正式版，还要价$29.99，实在说不过去。即使是为了给CUDA撑门面，也不用这么心急，多搞几轮beta测试不行么？