---
id: 175
title: FontRouter2前瞻之三 —— 重铸核心 海纳百川
date: 2006-12-02T01:53:53+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/12/02/fontrouter-preview-3/
permalink: /2006/12/02/fontrouter-preview-3/
dsq_thread_id:
  - "250426724"
  - "250426724"
categories:
  - Development
  - Symbian
tags:
  - Compability
  - FontRouter
  - OFS
  - Preview
  - Symbian
---
　　FontRouter2最本质的变化，也是让我下定决心重写全部代码的主要原因，是FontRouter2采用了与旧版本全然不同的核心机制。

　　如果将以往FontRouter的核心机制称作“替代式 (Override)”的话，那么FontRouter2所采用的则是“插入式 (Injection)”。技术层面的东西说起来比较晦涩，就让我们看看新内核所带来的变化吧。

<!--more-->　　首先，FontRouter2不再读取并识别字体文件，而是直接借用系统本身的字体辨识机制。这样，FontRouter2就彻底摆脱了以往常被广大机友所诟病的重复读取字体文件问题，籍由Symbian本身的字体点阵服务(Font Bitmap Server)统一管理。另一个感受得到的好处是，字体文件不再被锁定，通过众所周知的“更名父文件夹”的技巧，我们便可以在运行期间删除或者移动字体文件，一改以往不得不通过读卡器（或别的方式）替换字体的麻烦。其实，这背后还有一个现在很难体会到的更深层的优势：FontRouter2不再需要实现原本字体点阵服务已经完成的字体管理工作，将来即使增加了新的字体格式，只要安装相应的OFS插件，FontRouter2无需任何改变即可支持新的格式了。这一点无疑是兼容性上的一个重大跨越！

　　其次，FontRouter2实现了理论上Symbian OS中最广泛的版本兼容：从N9210年代古董级的Symbian 6.0，到现下流行的Symbian 8.1a；从S60v1、S60v2 FP1/FP2/FP3、S80、S90，再到UIQ。基本上除了Symbian 9（对应的S60v3、UIQ3）以外，均实现了期望中的完全兼容，而且是真正意义上的“二进制兼容” —— 一个文件，全部通吃！(: 可能有的朋友就会问，为什么要“除了”Symbian 9 呢？其实，FontRouter2已经实现了对Symbian 9 的源码级兼容。但作为Symbian OS发展史上的一次重大升级，Symbian公司作了一个非常残忍的决定——放弃了从Symbian诞生以来就一直得以保持的最大限度“二进制兼容”，援引Symbian 9 SDK中的兼容性描述：“New compiler and tool chain &#8211; **full binary break**”。无奈，这是任何一个Symbian程序员都无法跨越的编译器级的鸿沟……