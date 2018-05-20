---
id: 140
title: Symbian 9.2开始支持亚象素字体渲染技术(Sub-pixel font rendering)
date: 2006-10-23T23:08:56+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/10/23/symbian-92-support-sub-pixel-font-rendering/
permalink: /2006/10/23/symbian-92-support-sub-pixel-font-rendering/
dsq_thread_id:
  - "250426463"
  - "250426463"
categories:
  - Development
  - Symbian
tags:
  - Sub-pixel
  - Symbian
---
　　前几天下载了最新发布的Symbian 9.2 SDK文档，在浏览字体相关的改进时，无意中发现Enum TGlyphBitmapType继Symbian 7引入反锯齿字体渲染（EAntiAliasedGlyphBitmap）后，又新增了一个类型：亚象素字体渲染（ESubPixelGlyphBitmap）。

　　亚象素字体渲染技术是字体渲染技术运用在LCD上的一次重大进步，大家或许已经通过Acrobat/Adobe Reader中的ClearType体验过了亚象素渲染技术的效果，如下所示：

**普通的点阵字体渲染方式**

![Whole pixel rendered text](https://www.grc.com/image/ctpixel.gif)

**亚象素技术渲染后的效果（在非LCD显示器会得到完全不同的效果）**

![Sub-pixel rendered text](https://www.grc.com/image/ctsubpixel.gif)

　　当然，技术上支持并不意味着可以立即享受到这项改进，我们还需要等待Symbian在下一次更新字体渲染引擎（agfafontraster.dll或freetype.dll）时提供对亚象素字模格式的支持。