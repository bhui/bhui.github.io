---
id: 297
title: 仙剑四在17吋LCD上实现准全屏
date: 2007-12-19T01:26:44+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/12/19/play-pal4-in-nonscaled-full-screen/
permalink: /2007/12/19/play-pal4-in-nonscaled-full-screen/
dsq_thread_id:
  - "250427663"
  - "250427663"
categories:
  - Game
  - Software
tags:
  - ATI
  - Game
  - 仙剑
---
游侠网上有人给出了[仙剑四实现最高分辨率（1280&#215;960）下全屏的修改方法](http://game.ali213.net/thread-1597776-1-1.html)，但问题是现在的LCD恐怕没多少标准分辨率是这样的吧，如果直接按照这个方法全屏游戏，则会导致画面被垂直拉升（后果就不用我说了吧）。也不知道软星的开发人员怎么想的……

好在ATI的催化剂（Catalyst）控制中心提供了这样一项设置：Digital Panel (DVI) 3 &#8211; Attributes &#8211; Image Scaling，选择“Use centered timings”，然后再进入游戏即可享受到没有任何拉伸的“准全屏”效果了，相信上下那两条细细的黑边不会对你的游戏感受产生明显的影响吧。（特别是像我这台原本就黑色边框的LCD）

Nvidia的驱动不熟悉，不过相信也有类似的选项吧。:)