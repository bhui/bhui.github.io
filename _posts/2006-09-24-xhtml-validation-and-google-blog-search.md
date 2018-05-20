---
id: 123
title: XHTML认证与Google Blog Search
date: 2006-09-24T23:44:44+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/24/xhtml-validation-and-google-blog-search/
permalink: /2006/09/24/xhtml-validation-and-google-blog-search/
dsq_thread_id:
  - "250426344"
  - "250426344"
categories:
  - Development
  - Internet
tags:
  - Blog
  - Google
  - Search
  - XHTML
---
　　前两天抽空修正了原模版中大量的XHTML错误，终于完全通过了W3C的XHTML认证（[<img src="https://www.w3.org/Icons/valid-xhtml10" alt="Valid XHTML 1.0 Transitional" height="31" width="88" />](http://validator.w3.org/check?uri=referer)）。当初选择这个模版的时候，纯粹从美工的角度出发，没想到后来被模版中的XHTML错误给折腾惨了……

　　结果意外的是，自从XHTML错误修正后，Google Blog Search终于能够正常收录我的Blog了。以前就觉得纳闷，为什么被Google Blog Search收录的条目如此之少。在查阅了Support文档后，才知道原来它的Spider是基于RSS采集的，而不规范的XHTML页面将会导致Google Blog Spider无法正常识别到RSS链接。按理说，RSS链接是嵌入在HEAD部分中的，与BODY部分的内容的规范性关系不大。真是没想到Google竟然也有这么弱的时候……

　　另外，对模版中Widgets进行了重排和整理，调整了各个模块出现的时机（主要区分Home / Single Post），在Single Post中加入了“Related Posts”这个功能，主要基于UltimateTagWarrior插件实现。