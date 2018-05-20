---
id: 270
title: 关于E90的多媒体能力
date: 2007-09-06T02:11:57+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/09/06/multimedia-of-e90/
permalink: /2007/09/06/multimedia-of-e90/
dsq_thread_id:
  - "250427573"
  - "250427573"
categories:
  - Mobile
  - Symbian
tags:
  - Codec
  - E90
  - H.264
  - N95
  - OMAP2420
  - PowerVR
  - TI
  - 多媒体
---
眼下，E90与N95分别代表着Nokia两大系列中的顶级配置，提到E90的多媒体性能，最直接的较量者无非就是N95了。

从Nokia官方的参数看，E90与N95均内置硬件图形加速，确切的说，是采用了经过PowerVR授权的TI OMAP2420芯片。其中所内含的MBX/VGP模块就是硬件图形加速的主角。根据<a href="http://en.wikipedia.org/wiki/PowerVR" target="_blank">Wikipedia上的PowerVR资料</a>，E90是E系列唯一采用硬件图形加速的型号，而N系列则还包括N95之外的N93、N93i、N800。可见，面对即将到来的下一代N-Gage游戏平台，E90是N系列之外的唯一的入围者。

PowerVR芯片除了支持手机游戏所需的OpenGL ES接口外，另一个重要的用途则是视频编解码的硬件加速了。根据<a href="http://wiki.forum.nokia.com/index.php/Codecs" target="_blank">Nokia官方Wiki的资料</a>，N95与E90拥有完全相同的Video Codec支持，包括RealVideo 8/9/10、H.263/MPEG4、H.264。

为了证实视频解码的硬件加速效果，我做了一系列简单实验：（均采用内屏全屏）

（1）用内置的RealPlayer播放全屏MPEG-4视频《变形金刚》预告片，非常流畅；
  
（2）用CorePlayer播放上述预告片，不流畅；
  
（3）用SmartMovie播放一段Xvid视频《Island》（HD转Xvid全屏），不流畅；
  
（4）用CorePlayer播放上述预告片，流畅。

总体来说CorePlayer的解码性能超过SmartMovie，但播放MPEG-4的流畅度却不如内置的RealPlayer。比较合理的解释应该是RealPlayer使用了系统提供的Video Codec解码MPEG-4影片，也就是说运用了硬件加速。

不过在尝试播放全屏的H.264的影片时，RealPlayer虽然识别到文件格式，但却提示“无法播放” ，CorePlayer倒是能播放，不过其速度可就惨不忍睹了。（毕竟在PC上软解码H.264都是一件比较吃力的活儿……）

目前还不清楚制作内置RealPlayer能播放的H.264影片需要什么条件，有成功经验的朋友还望不吝赐教！