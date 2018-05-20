---
id: 200
title: FontRouter2 for Symbian 9 is incoming!
date: 2007-02-14T02:22:40+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/02/14/fontrouter2-for-symbian9-is-incoming/
permalink: /2007/02/14/fontrouter2-for-symbian9-is-incoming/
dsq_thread_id:
  - "250426894"
  - "250426894"
categories:
  - Development
  - Symbian
---
　　这几天花了很长时间研究Symbian 9的Open Font System接口变化，总算小有收获。话说这Symbian 9打算以ECOM框架一统全部插件接口，OFS当然也被收编其下。但SDK文档中几乎所有关于OFS接口的说明却仍然停留在旧的接口下，这让我非常困惑。经过几天来对UIQ3和S60 v3的彻底分析和反汇编，终于找到了移植OFS插件至Symbian 9的正确途径，目前已基本在上述两个平台下实现了FontRouter2的正确加载，后面将开始进行功能的调试。

　　今天的分析还得出了另一个重要的结论：Nokia S60 v3并非如很多人想象的那样不借助OFS即可支持TrueType字体，事实上，与早期的FreeType和中期的AgfaFontRaster一样，S60 v3也同样存在这样一个用以支持TrueType的OFS插件，只不过改名易姓成了“iTypeRast”，在ROM中的sysbin下可以找到它。

　　由于Symbian 9非常特殊的安全机制，我尚无法确定FontRouter2在模拟器中的表现与实机存在多大差别，为了顺利推出FontRouter2 for Symbian 9，现在希望提前征集数名测试志愿者，希望得到大家的支持和协助，谢谢！:)