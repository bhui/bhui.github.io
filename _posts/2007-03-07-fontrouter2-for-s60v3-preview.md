---
id: 215
title: 搞定FontRouter2 @ S60v3
date: 2007-03-07T02:10:39+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/03/07/fontrouter2-for-s60v3-preview/
permalink: /2007/03/07/fontrouter2-for-s60v3-preview/
dsq_thread_id:
  - "250427022"
  - "250427022"
categories:
  - Development
  - Symbian
---
　　今天终于彻底解决了S60v3上[FontRouter2无法拦截到部分字体请求的问题](http://blog.oasisfeng.com/2007/02/27/fontrouter2-for-symbian9-preview/)（这个问题其实也存在于原S60第二版的环境下），还是多亏IDA帮了大忙。到目前为之，已初步在模拟器上完成FontRouter2向Symbian 9下两个平台——S60v3和UIQ3的移植验证。

　　大家看到下面这个图一定会猜想“哇，这是什么界面语言？” 呵呵，其实模拟器里跑的还是英文版的S60v3，只不过我让FontRouter2运行在一个特殊的调试模式下，以方便验证是否成功拦截了所有的字体请求。至于下面这些字符是代表什么含义，相信聪明的你早已猜出来了吧~ 🙂

<center>
  <img src="https://blog.oasisfeng.com/wp-content/uploads/2007/03/fontrouter2s60v3.jpg" alt="Preview: FontRouter2 for S60 3rd Edition" />
</center>