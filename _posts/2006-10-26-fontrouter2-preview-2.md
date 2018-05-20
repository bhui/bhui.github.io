---
id: 143
title: FontRouter2前瞻之二 —— TrueType与点阵字体的双剑合璧
date: 2006-10-26T22:33:33+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/10/26/fontrouter2-preview-2/
permalink: /2006/10/26/fontrouter2-preview-2/
dsq_thread_id:
  - "250426479"
  - "250426479"
categories:
  - Development
  - Symbian
tags:
  - FontRouter
  - Symbian
---
　　对TrueType字体的完美支持（通过FreeType插件）是FontRouter2最重要的改进之一。众所周知，TrueType字体是一种流行的矢量字体格式，拥有大量的字体资源，倘若能用TrueType字体作为手机的界面字体，那么自然再也不用为可供选择的字体太少而发愁了。

　　在最初发布FontRouter的时候，Symbian智能手机上就已经可以支持TrueType字体了，在[FontRouter的发布贴](http://www.wda.com.cn/viewthread.php?tid=105356)中我也解释了如何在Symbian下实现对TrueType字体的支持。但当时大部分Symbian手机所配备的100Mhz的ARM4 CPU其实难以胜任中文TrueType字体所需的高强度矢量计算，英文TrueType字体的显示速度虽然尚可接受，但显然并不是大家所关注的方向。因此，FontRouter前期的版本并没有提供对TrueType字体的支持。

　　时过境迁，如今的Symbian智能手机的硬件配置早已发生了翻天覆地的变化，新一代机型普遍配备的200MHz ARM5 CPU和高达32M的RAM足以支撑中文TrueType字体的矢量运算，就连开启反锯齿效果都胜任有余。在这样的背景下，对TrueType字体的支持就自然而然的成为了大家最期待的功能。TrueType字体与点阵字体的同屏显示、自由取舍、按需搭配 理所当然的成为了FontRouter2相对NOKIA/Symbian原生支持的强劲优势！

　　Symbian从7.0开始支持TrueType字体的反锯齿渲染效果，这项改变对字体显示，特别是在手机这种小尺寸LCD上，所带来的效果提升绝对是激动人心的！对比下面两幅图片就可以看出其中的巨大差别来：

左图界面字体开启了反锯齿效果，右图窗口中的文字则关闭了反锯齿效果：

<center>
  <img src="https://blog.oasisfeng.com/wp-content/uploads/2006/09/n70_1.jpg" alt="Anti-aliased" />&nbsp;<img src="https://blog.oasisfeng.com/wp-content/uploads/2006/09/n70_3.jpg" alt="Monochrome" />
</center>

　　让我们一起期待FontRouter2即将带来的TrueType字体潮流吧！