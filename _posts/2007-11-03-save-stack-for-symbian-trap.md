---
id: 280
title: 在栈空间敏感的环境中应谨慎使用TRAP()
date: 2007-11-03T10:26:39+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/11/03/save-stack-for-symbian-trap/
permalink: /2007/11/03/save-stack-for-symbian-trap/
dsq_thread_id:
  - "257845778"
  - "257845778"
categories:
  - Development
  - Symbian
tags:
  - Leave
  - Stack
  - Symbian
  - TRAP
  - TRAPD
  - 栈
---
最近在优化一个函数的栈使用中，意外的发现以前一直被忽略的一个消耗源，那就是TRAP()宏。作为Symbian编程基石之一的TRAP/Leave在已经被很多人当作C++的try{throw}catch一样使用的时候，你是否意识到这个宏会消耗多达76字节的栈空间？如果使用的是TRAPD()版本，则这个数字将达到80字节。倘若函数中用了不止一次的话，栈消耗将相当可观。

除了认真审视函数上下文中是否有使用TRAP()的必要（有些时候直接往上传递Leave也未尝不可）， 可能更多的时候是难以避免使用TRAP()的，那么如何才能尽量节省栈空间呢？这里有一个简单的方法，那就是把TRAP()宏拆开来，在一个函数内使用共享的TTrap对象。

如果你也被Symbian那点可怜的栈空间困扰，不妨也关注一下程序中TRAP()/TRAPD()的使用吧。