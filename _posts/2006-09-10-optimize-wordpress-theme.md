---
id: 104
title: 略微优化了一下WordPress模版
date: 2006-09-10T21:19:23+00:00
author: oasisfeng
layout: post
guid: 'http://blog.oasisfeng.com/2006/09/10/%e7%95%a5%e5%be%ae%e4%bc%98%e5%8c%96%e4%ba%86%e4%b8%80%e4%b8%8bwordpress%e6%a8%a1%e7%89%88/'
permalink: /2006/09/10/optimize-wordpress-theme/
dsq_thread_id:
  - "258663310"
  - "258663310"
categories:
  - Internet
tags:
  - WordPress
---
　　今天抽了一点时间略微优化了一下这个WordPress模版，主要是将最近这段时间使用中发现的bug修正了，把不足改进了。一些较大的调整仍在规划中，希望加入部分改善使用体验的AJAX特性。

<!--more-->　　首先，还是字体问题，上次只把文章主体部分字体的大小修改了，但是原模版这个font-family让我觉得始终有些别扭，于是重新按照自己的审美观和页面布局的需要调整了CSS中大部分的字体设定。这样看起来总算不那么另类了。

　　其次，是页面标题的问题，由于原模版默认完整页面的标题是“Blog Name + ‘Blog Archive’+ Post Title”，这样不仅显得非常冗余，而且在搜索引擎的搜索结果列表中甚至只能看到一半的Post标题（超长截断……）。因此，着手调整为“Post Title + Blog Name”的样式，这样不仅改善了读者体验，而且也更显[搜索引擎亲和](http://theundersigned.net/2006/06/wordpress-and-seo/)。不过颠倒顺序后倒是在分隔符上遇到了一点小小的问题，TITLE需要按照[这里提到的方式](http://theundersigned.net/2006/06/wordpress-and-seo/)修改才能解决。

　　然后，重新规划了右边的Widges，去掉了意义不大的Recent Posts，改为Random Posts，并用WP的Link &#8211; BlogRoll实现了My Friends这一栏，排名不分先后（其实就是乱序排列)。优化了一下显示效果，看起来跟原Blogger上差不多了。（不过总觉得布局上还有一点杂乱的感觉，可能是CSS没有仔细优化的缘故吧&#8230;）

　　另外，把文章标题左侧的日历样式调整了一下，让它看起来更中国化一些了。

　　别的一些零碎的修改我也不记得了，呵呵，反正是看着哪儿不爽就改哪儿。