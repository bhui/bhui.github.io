---
id: 46
title: FontRouter新版本计划已启动
date: 2006-06-25T18:00:10+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/06/25/fontrouter%e6%96%b0%e7%89%88%e6%9c%ac%e8%ae%a1%e5%88%92%e5%b7%b2%e5%90%af%e5%8a%a8/'
permalink: /2006/06/25/started-plan-of-new-fontrouter/
dsq_thread_id:
  - "250426051"
  - "250426051"
categories:
  - Development
  - Symbian
tags:
  - FontRouter
  - Symbian
---
　　时隔一年多，终于在最近重新启动了FontRouter的新版本计划。尽管工作依旧很忙，但我仍希望能在每天晚上下班后抽出一两个小时的时间继续进行开发，为这个沉寂已久的软件带来一些新的活力。

　　新版本主要关注的方向是：

<!--more-->　　（1）消除原有的bug并解决兼容性问题，争取实现真正意义上的全Symbian兼容，包括S80、S90及新的S60v3；

　　（2）支持挂接其他OFS插件（包括FreeType），并纳入FontRouter的管理机制中；

　　（3）支持更多新特性，例如字体的动态卸载/加载、防白屏保护机制、应用程序的字体定制……

　　（4）增加API接口，并编写相应的前台用户界面，实现字体的配置和管理；

　　（5）……

　　前面几天的时间主要花在重构核心部分的代码，并再次对字体的动态卸载作出尝试。可惜的是，虽然实现了英文字体的动态卸载，但对于中文字体，却始终未能成功。从内存分配的跟踪分析来看，Symbian对于含有大量Code Section的中文字体处理上似乎有些特别之处，估计是为了加速点阵查找而在内存中为其创建了某种形式的索引（在第一次调用GetNearestFontInPixels()时，如果是英文字体，则仅有为CBitmapFont分配内存的请求；而对于中文字体，却跟踪到了数千个新的内存分配请求）。该索引在字体卸载后似乎并未从内存中释放（缓存了？），导致其引用的实际内存地址不可用。Symbian的内核部分实在开放的太少，字体的核心处理又隐藏的太深，让人很难摸透个中玄机……后续我还会继续就这个问题进行尝试，希望能找到突破。