---
id: 464
title: 自制简易Portable Putty
date: 2008-10-08T22:42:43+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=464
permalink: /2008/10/08/my-portable-putty/
dsq_thread_id:
  - "250427872"
  - "250427872"
categories:
  - Computer
tags:
  - portable
  - putty
---
重装系统后，Putty站点信息又丢失了……原来Putty的配置数据是保存在注册表中的。在网上找了一下解决方案，看到不少推荐Portable Putty的。从它的官方Modification介绍中看出，是套了一个Loader维护注册表项的加载和保存。下载来安装后发现这个东西每次启动竟然还要弹出一个Splash，真是有点恶心。

对比了一下Portable Putty中的putty.exe，发现竟然和原版的大小不同。非吾疑心太重，怎奈而今互联网实在水深不浅，不可不防。官方网站上倒是给了一个“颇为官方”的说法：

> The PuTTY EXE was recompressed using UPX.

我要是想捆绑木马，也会用UPX来伪装一下的。鉴于上述两个原因，遂弃之不用。

<!--more-->自己动手写了一个简单的批处理，作为Putty的启动外壳：

> @echo off
  
> rem Export settings and saved sessions in registry.
  
> regedit /e %CD%putty.reg HKEY\_CURRENT\_USERSoftwareSimonTatham
  
> start putty.exe 

虽然只在启动前备份，显得很不专业，但对于像我这样大部分时候不会去修改设置的人来说还是足够了。另外也不用担心第一次启动时会覆盖以前的注册表导出文件，即使启动后发现没有配置了，退出来导入putty.reg文件就行了。

* * *

**UPDATE:** 找到一个[国外热心网友做的patch](http://jakub.kotrla.net/putty/)，支持文件方式存储session，网站上提供有源码及编译好的版本。唉，为啥没早发现它呢……