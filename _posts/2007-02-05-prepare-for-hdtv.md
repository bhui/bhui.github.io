---
id: 196
title: 步入HDTV时代
date: 2007-02-05T23:35:39+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/02/05/prepare-for-hdtv/
permalink: /2007/02/05/prepare-for-hdtv/
categories:
  - Computer
tags:
  - 1080p
  - CoreAVC
  - H.264
  - HDTV
  - KMPlayer
  - MPEG2
---
　　HDTV的时代快要来临，你做好准备了么？

　　昨天入手了一块新硬盘，总算不必再被容量所困扰。现在，除了显示器，其它部件已基本具备HDTV的要求了~ （就等24&#8243; LCD降价……）

　　主机乃是两年前配置的：

> CPU: AMD Athlon64 2800+ (OC 3200+)
  
> 主板: ASUS K8N
  
> RAM: DDR 1G (1T)
  
> 显卡: ASUS 9550 256bit/128M (250/400 MHz)
  
> LCD: 17&#8242;
  
> 硬盘: 希捷7200.10 320G/16M

　　用KMPlayer + CyberLink MPEG2 Decoder(PD7) + CoreAVC 1.2的组合分别测试播放MPEG2和H.264的HDTV（均为1080p）。

**MPEG2: 使用CyberLink**
  
　　开启ATI的硬件MPEG2解码后，效果非常明显，可以达到全速下40%左右的CPU占用率。而一旦关闭硬件解码，CPU占用率立即飙升至100%……

**H.264 @ 12Mbps: 使用CoreAVC**
  
　　关闭deblocking、硬件dx-deinterlacing，可以达到全速下80%的CPU占用率。此时画质尚可，但在场景高速变换时会出现明显的方块。
  
　　b-frame deblocking、硬件dx-deinterlacing，可以达到全速下90%的CPU占用率。画质几乎没有损失，即使在高速场景中也察觉不到方块。
  
　　standard deblocking、硬件dx-deinterlacing，此时FPS大约22、CPU占用率100%，但个人感觉不到有丢帧。
  
　　关闭硬件deinterlacing几乎对FPS和CPU占用率没有影响，所以有显卡相助，何乐而不为呢？:) 另外，大家评价很高的CyberLink H.264 Decoder在我这里的表现却不尽如人意，没有deblocking、时不时卡一下不说，还与 ASUS Splendid 冲突……

　　看来，这台两年前配置的电脑基本上还能应付常规的HDTV播放需求，但面对高bps的H.264影片估计就扛不住了。