---
id: 187
title: Symbian终于开始兼容POSIX
date: 2007-01-25T00:13:23+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/01/25/posix-on-symbian/
permalink: /2007/01/25/posix-on-symbian/
dsq_thread_id:
  - "250426799"
  - "250426799"
categories:
  - Development
  - Symbian
tags:
  - EPOC
  - POSIX
  - Symbian
  - WinCE
---
Official news: [Symbian introduces POSIX libraries on Symbian OS](http://www.symbian.com/news/pr/2007/pr20078721.html)

　　Symbian终于放下高贵的“架子”，开始变得对开发者平易近人。“兼容POSIX”是在这一演变过程中迈出的具有里程碑意义的重要步伐。

　　Symbian诞生之初（可以追述到当初的EPOC），是针对掌上型资源高度受限设备所开发的。为了最求极致的性能发挥和最小的资源消耗，它从操作系统内核到编程框架都进行了严苛的优化，甚至对C++的不少基本机制也进行了大刀阔斧的革新。这些优化足以让Symbian在面对WinCE时显示出压倒性的性能优势，并成为了Symbian最初在拉拢智能手机生产厂商时的核心竞争力。（想想老一代的WinCE吧，那简直是“耗电量大”、“响应迟钝”的代名词，连Palm都不如……）

　　随着时间的迁移，Symbian的性能优势已被不断改善的手持终端硬件条件所逐渐抹平。而WinCE平台以其开发门槛低、可移植性高等现实优势迅速的羽翼丰满起来。面对竞争压力，Symbian不得不抛开过于完美化的前卫理念，从放宽License条件到提供兼容全局变量的解决方案，Symbian在保持其优雅构架的同时，也开始向“传统”敞开大门。这次对POSIX兼容结构的支持终于算是迈出了关键的一步。从此，大量的桌面应用，特别是侧重算法类的应用都可以更加轻松的移植到Symbian平台，为本已非常丰富的Symbian应用软件世界注入新的活力！