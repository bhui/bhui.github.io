---
id: 49
title: 终于让Source Insight也能识别Symbian的_LIT宏了
date: 2006-05-27T17:56:02+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/05/27/%e7%bb%88%e4%ba%8e%e8%ae%a9source-insight%e4%b9%9f%e8%83%bd%e8%af%86%e5%88%absymbian%e7%9a%84_lit%e5%ae%8f%e4%ba%86/'
permalink: /2006/05/27/parse-lit-in-source-insight/
dsq_thread_id:
  - "256279556"
  - "256279556"
categories:
  - Development
  - Symbian
tags:
  - Development
  - Source-Insight
  - Symbian
---
　　不得不承认，Source Insight 确实很强大，以至于太多的高级功能都未能在帮助文档中一一详述，只能依靠我们自己来发掘了……

　　今天，碰巧发现了&#8221;Language &#8211; Custom Tag Type&#8221;这个功能，一举解决了困扰我已久的 Symbian &#8220;_LIT&#8221;宏解析问题。（也不知道是否因为我的 Conditions 定义的不足导致的……）

　　长话短说，&#8221;Options &#8211; Document Options&#8221;，新建一个&#8221;Document Type&#8221;，如&#8221;Symbian C++ Source Files&#8221;，继承原有&#8221;C++ Source Files&#8221;的属性。然后在左下角&#8221;Parsing&#8221;设置组中的&#8221;Custom Tag Type&#8221;下选择&#8221;Constant&#8221;，并将下面的正则表达式填入&#8221;Custom pattern&#8221;：

　　**^w\*_LIT(w\*([A-Za-z0-9]+)w\*,.\***

　　OK, resynchronize your project, you&#8217;ll see it!

　　注：记得将 Document Type 中原 c 和 cpp 的 File Filter 项里面的扩展名 .cpp 和 .h 屏蔽掉，否则 SI 不会调用我们新建的 Document Type 来解析的。