---
id: 208
title: 'Preview: FontRouter2 for Symbian 9'
date: 2007-02-27T02:03:55+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/02/27/fontrouter2-for-symbian9-preview/
permalink: /2007/02/27/fontrouter2-for-symbian9-preview/
dsq_thread_id:
  - "250426985"
  - "250426985"
categories:
  - Development
  - Symbian
---
　　总体来说，移植过程还算基本顺利，除了[前面提到的THeapWalk](http://blog.oasisfeng.com/2007/02/23/theapwalk-for-symbian9/)。由于Scalable UI的引入，Open Font System接口也引入了不少新的变化，最主要的新特征是字体获取接口衍生为三个：旧接口依旧保留，但不会被Symbian 9调用（怀旧兼容？），两个新增的接口分别用于根据“设计高度(Design Height)”和“最大高度(Max. Height)”获取字体。这两个新概念显然也是为Scalable UI服务的。

　　今天晚上，基本在UIQ3模拟器下成功调试通过了，从Opera浏览器中的中文表现来看，FontRouter2的核心功能已经正常实现了。

<center>
  <img src="https://blog.oasisfeng.com/wp-content/uploads/2007/02/fontrouter2uiq3.jpg" alt="FontRouter2 on UIQ3" />
</center>


  
　　不过在S60第三版上却遇到了一些麻烦：首先是与Nokia的iTypeRast存在一定的兼容性问题，出现了“缺字”现象（在第二版的AgfaFontRaster上也有类似兼容性问题），其次还是iTypeRast，竟然在部分字体的竞争中压过了FontRouter2。实在汗啊，看来iTypeRast也开始不择手段了…… 或许确实有必要做一些比较极端的屏蔽手段来对付iTypeRast了。今天也不早了，好在这两个问题都能在模拟器中重现，所以就明天再来详细分析吧。