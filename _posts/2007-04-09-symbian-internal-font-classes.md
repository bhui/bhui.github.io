---
id: 232
title: 初步完成Symbian全部字体相关内部类结构的反向工程
date: 2007-04-09T00:43:38+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/04/09/symbian-internal-font-classes/
permalink: /2007/04/09/symbian-internal-font-classes/
dsq_thread_id:
  - "250427218"
  - "250427218"
categories:
  - Development
  - Symbian
---
经过几个月的逐步积累，终于初步完成了所有这些字体相关类的结构整理和少量简单成员方法的反汇编。包括但不限于：

CFontStoreFile
  
CFontBitmap
  
TTypefaceFontBitmap
  
TOpenFontFileData
  
COpenFontSessionCacheList
  
COpenFontGlyph
  
COpenFontGlyphTreeEntry
  
COpenFontGlyphCache
  
COpenFontSessionCacheEntry
  
COpenFontSessionCache
  
COpenFontSessionCacheListItem
  
COpenFontSessionCacheList
  
COpenFontPositioner (Deprecated)
  
TKern (Deprecated)
  
TLigature (Deprecated)
  
TDiacritic (Deprecated)

终于不必再因为Symbian那少的可怜的字体API接口而进行缚手缚脚的Coding了~

待后续验证和测试通过后，我会逐步公开这些Symbian内部接口。（仅供教学和研究用途）

* * *After months, I&#8217;ve finally finished preliminary reverse-engineering analysis on all the font-related internal classes in Symbian. After basic validation and test, I&#8217;ll publish all the analysis results, only for educational purpose.</p>