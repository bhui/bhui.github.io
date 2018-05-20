---
id: 117
title: 避免WordPress转换空格及特殊字符
date: 2006-09-20T00:50:17+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/20/avoid-char-conversion-by-wordpress/
permalink: /2006/09/20/avoid-char-conversion-by-wordpress/
dsq_thread_id:
  - "250426293"
  - "250426293"
categories:
  - Internet
tags:
  - pre
  - WordPress
---
　　经常用WordPress发表技术文章，特别是程序代码的朋友或许都曾遇到过引号、双减号等特殊字符被自动替换为全角符号的问题，而且空格也会被压缩。虽然使用 code 标签可以避免字符转换的问题，但仍然不能解决空格压缩，使得代码的缩进效果看起来很糟糕。虽然有一些专用插件可以避免上述问题，但不符合我个人“Simple is the best!”的理念。

　　今天在反复尝试后，终于找到了一个简单的办法完全解决上述两个问题，那就是使用“pre”标记。“pre”是早期HTML标准中用来指示“原样引用”的标记，取“preservation”的缩写。所有包含在＜pre＞和＜/pre＞之间的内容都将原样保留，包括连续的空格，也不会出现特殊字符被转换的情况。对比如下：（两行中书写的实际内容相同）

未用pre标签：

app &#8211;param=&#8221;string&#8221;

使用pre标签：

<pre>app --param="string"</pre>

注：pre是“区块”标签，因此不能用于行内的局部。