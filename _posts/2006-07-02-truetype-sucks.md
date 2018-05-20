---
id: 44
title: TrueType，想说爱你不容易……
date: 2006-07-02T16:29:39+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/07/02/truetype%ef%bc%8c%e6%83%b3%e8%af%b4%e7%88%b1%e4%bd%a0%e4%b8%8d%e5%ae%b9%e6%98%93%e2%80%a6%e2%80%a6/'
permalink: /2006/07/02/truetype-sucks/
dsq_thread_id:
  - "286165482"
  - "286165482"
categories:
  - Development
  - Symbian
tags:
  - FontRouter
  - Symbian
  - TrueType
---
　　在搞定了字体的动态加载/卸载后，周末对最后一项可行性实验——“集成FreeType支持”发起了挑战。虽然对困难有足够的估计，但是FreeType的叛逆还是让我很恼火。因为Symbian没有提供WINS版本的FreeType.dll，导致无法直接在模拟上进行调试。也罢，自己写了一个Dummy来模拟FreeType.dll的行为，然后一举在模拟器上调试通过。如此“顺利”的进展也让我多少有点意外，哪知道上机测试即告失败。启动时直接卡在“NOKIA”几个大字阶段，漫长的等待后——“白屏”……

　　好在本次项目启动后所完成的第一个特性就是“防白屏保护”，让我免除了后顾之忧。还记得一年前因为存着侥幸心理，结果调试FontRouter的过程中NG白屏过两次，造成高达数十元RMB的直接经济损失以及往返于“通天地”的奔波之苦，最后还落得收音功能实效的后遗症……

　　开源的FreeType项目在被Symbian移植后，不但拒绝开源不说，甚至连模拟器上的DLL版本都不提供，如此讳莫如深，让人多少有些感叹Symbian和开源的潮流实是相去甚远……