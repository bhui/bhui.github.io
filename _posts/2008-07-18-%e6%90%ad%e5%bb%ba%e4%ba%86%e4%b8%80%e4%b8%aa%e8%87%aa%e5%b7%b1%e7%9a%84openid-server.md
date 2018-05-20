---
id: 340
title: 搭建了一个自己的OpenID Server
date: 2008-07-18T23:08:14+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=340
permalink: '/2008/07/18/%e6%90%ad%e5%bb%ba%e4%ba%86%e4%b8%80%e4%b8%aa%e8%87%aa%e5%b7%b1%e7%9a%84openid-server/'
dsq_thread_id:
  - "250427836"
  - "250427836"
categories:
  - Internet
tags:
  - openid
  - PHP
---
利用开源的[phpMyID](http://siege.org/projects/phpMyID/)搭建，以域名“id.oasisfeng.com”作为[OpenID](http://www.openid.net/)的认证标志，简单易记。从此不必依赖互联网上的公共OpenID服务商，也不用担心各种各样的潜在隐私问题。当然，带价是得自己防范黑客攻击。

PS：本来搭建的步骤非常简单，结果给phpMyID的README里那一大堆废话给反而搞复杂了……

补充：其实还可以用更简短的“oasisfeng.com”作为认证标志，前提是你可以通过这种不带“www”前缀的URL访问自己的域名，然后只要在这个域名首页HTML的<HEAD>部分中插入如下内容（从http://id.oasisfeng.com/在浏览器中看到的源码中复制过来）即可：

<pre>&lt;link rel="openid.server" href="http://id.oasisfeng.com/" /&gt;
&lt;link rel="openid.delegate" href="http://id.oasisfeng.com/index.php" /&gt;</pre>