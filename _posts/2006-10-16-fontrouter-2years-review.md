---
id: 135
title: FontRouter两周年回眸
date: 2006-10-16T22:46:29+00:00
author: oasisfeng
layout: post
guid: 'http://blog.oasisfeng.com/2006/10/16/fontrouter%e4%b8%a4%e5%91%a8%e5%b9%b4%e5%9b%9e%e7%9c%b8%e2%80%94%e2%80%94%e6%bf%80%e6%83%85%e7%87%83%e7%83%a7%e7%9a%84%e5%b2%81%e6%9c%88/'
permalink: /2006/10/16/fontrouter-2years-review/
dsq_thread_id:
  - "250426434"
  - "250426434"
categories:
  - Development
  - Symbian
tags:
  - FontRouter
  - Symbian
---
　　回顾FontRouter的发展历程，转眼已经历了两度春秋。

　　2004年，那段激情燃烧的岁月里，经过好友的推荐，我来到了当时国内最大的Symbian智能手机论坛“[WDA中文网](http://www.wda.com.cn)”。针对Symbian中文本地化支持的研究潮流在那时几乎长期居于WDA学术氛围的主导地位，涌现了很多像hsz76、tomken这样为着Symbian中文优化不懈努力的斗士，他们对Symbian中文支持力求完美的精神深深打动了那时才刚刚接触Symbian的我。FontRouter的计划就是在这样的背景下诞生的。

　　[2004年10月15日，FontRouter 0.1 beta 在WDA上发布了。](http://www.wda.com.cn/viewthread.php?tid=105356)虽然这个版本尚没有真正运用Open Font System的力量，但它所创造的影响已经为FontRouter赢得了众多的支持者。“从MMC卡加载字体”这一重要的突破为当时所有研究Symbian字体的斗士们带来了福音，因为那时候对字体的不慎修改常常会导致NG上最可怕的灾难——白屏。一旦字体可以从MMC卡加载，就意味着可以从此远离“白屏”的烦恼了！

　　2004年10月18日，FontRouter 0.8 beta 诞生了。为什么我用“诞生”这个词来描述这一版本的发布呢？那是因为，从0.8开始，FontRouter首次完全实现了通过Open Font System构架对中英文字体混合显示的支持。这一实现方式从根本上颠覆了当时以字体修改为手段的Symbian中文化研究思想，它所带来的影响甚至直接超越了NOKIA官方提供的中文支持。

　　中英文字体混合显示，同屏渲染的效果绝非NOKIA中文版手机所能比拟的。用过英文版机型的朋友或许都会对多样化的英文字体效果情有独钟，LatinPlain12、LatinBold12、LatinBold13、LatinBold17、LatinBold19五种界面字体共同塑造出了Symbian优雅的英文字体风格。可惜的是，当相应的英文机型被NOKIA中文化之后，为了屈就于中文字体的尺寸，五种英文字体被“缩减”成了两种，而且字模也远没有原英文字体美观。更可笑的是，在NOKIA中文机型中，部分应用软件或者Java程序竟然会出现中文显示为“口口”的情况。FontRouter的出现从根本上扭转了这一局面，从此中英文字体的显示风格可以相得益彰，从此无论应用软件还是Java程序都告别“口口”。以致于在相当长一段时间内，发烧级的S60机友甚至偏爱英文+FontRouter更甚中文机型。

　　注：“口口”是当Symbian在当前字体中找不到Unicode对应的字模时采用的替代符号，形如“口”而得名。

[待续&#8230;]