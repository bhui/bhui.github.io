---
id: 111
title: 改善WordPress的Google亲和力——Google Sitemaps
date: 2006-09-16T14:54:06+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/16/wordpress-plugin-google-sitemaps/
permalink: /2006/09/16/wordpress-plugin-google-sitemaps/
dsq_thread_id:
  - "250426292"
  - "250426292"
categories:
  - Internet
tags:
  - Google
  - Sitemaps
  - WordPress
---
　　这里我不是打算介绍什么是Google Sitemaps，你只需要知道它的作用——好比一篇呈给Google搜索引擎的自荐书。有了它，才能让Google对你的网站“刮目相看”！

　　从最近一段时间的Google Analytics分析报告来看，Blog访问量的一个重要来源就是Google的搜索结果（当然，也不排除Google Analytics“假装”不认识其它搜索引擎的可能）。而当我[用Google搜索自己的Blog](http://www.google.com/search?q=site%3Ablog.oasisfeng.com)时才发现展示出来的结果是如此糟糕，所有页面包括comments feed都杂乱无序的排列在一起，甚至当我翻阅搜索结果到第三页时才找到Blog的首页…… X-(

　　那么如何撰写一篇高质量的自荐书呢？Google给出了一份详细的Sitemaps参考手册，不过我是不打算去读完那么一篇冗长的文档了。好在已经有这么一个[WordPress下的Sitemaps插件](http://www.arnebrachhold.de/2005/06/05/google-sitemaps-generator-v2-final)可以自动帮我们完成这一繁琐的过程，我是无意中从[“般若个人空间”](http://blogbenny.dd.am/2006/08/14/23/)中发现它的。

　　经过Google Sitemaps的优化，[再回到Google搜索结果](http://www.google.com/search?q=site%3Ablog.oasisfeng.com)一看，整个焕然一新，而且Blog首页也跃然至首位。如果对搜索结果的排列顺序还不满意的话，可以在Options-Sitemaps中调节一下Priority的设置。

　　由于插件自动ping了Google的Sitemaps服务器，因此修改结果将在Google中即刻呈现。同时这个插件还会在每次发布新的Post时自动ping一次，所以Google搜索结果也将伴随着你的Blog更新与时俱进！;)