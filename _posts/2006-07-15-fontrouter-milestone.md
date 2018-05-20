---
id: 41
title: 峰回路转 柳暗花明
date: 2006-07-15T17:28:13+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/07/15/%e5%b3%b0%e5%9b%9e%e8%b7%af%e8%bd%ac-%e6%9f%b3%e6%9a%97%e8%8a%b1%e6%98%8e/'
permalink: /2006/07/15/fontrouter-milestone/
dsq_thread_id:
  - "400912929"
  - "400912929"
categories:
  - Development
  - Symbian
tags:
  - FontRouter
  - Symbian
  - TrueType
---
　　这半个月里，一直苦苦寻觅破解FreeType的良方而不可得，今天终于可以送一口气了。

　　当初遍寻Nokia S60、S80和S90系列的SDK，都没有找到FreeType.dll的WINS版本，后经过某大虾的提点，终于在UIQ3 SDK中捕捉到了它的踪影。刚兴奋没多久，尝试在S60 v1/v2中借用它时就失败了。其实结果是显而易见的，Symbian 9 修改了大量接口，与之配套的FreeType.dll直接拿到S60 v1/v2中来用时，自然会有很多关联的dll无法找到对应的ordinal。索性尝试将FontRouter port到UIQ3中来调用FreeType，结果又失败了（Symbian 9的门槛果然比较高，这个短期内暂不考虑了）……郁闷之余，甚至还尝试过反汇编它，依然未果……

　　今晚，在寻找一个稀有的头文件时，灵感突发。因为涉及一些被Nokia隐藏的内部接口时，常常能从早期的SDK版本中找到所需的头文件（后来的版本中被去掉了），比如Moto A920、N9200以及传说中的Sendo SDK。那么，Freetype.dll是否也如出一辙呢？于是乎，搬出所有收藏的古董级SDK统统装上。果不其然，让我在N9200 SDK中找到了WINS版本的FreeType.dll。哈哈，有了这把钥匙后，剩下的攻势自然势如破竹，不到1个小时就在模拟器上调通了。当那带着几分晦涩却又让人无限神往的TrueType字体浮现在EPOC的窗口中时，我缓缓坐下来，呷了一口杯中的绿茶，闭上双眼，细细品位这一刻的舒畅……