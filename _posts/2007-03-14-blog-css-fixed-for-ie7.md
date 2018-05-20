---
id: 218
title: 修复Blog在IE7下的显示问题
date: 2007-03-14T20:55:50+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/03/14/blog-css-fixed-for-ie7/
permalink: /2007/03/14/blog-css-fixed-for-ie7/
dsq_thread_id:
  - "250427032"
  - "250427032"
categories:
  - Internet
---
因为用惯了Firefox，再加上兼容性方面的原因，一直没有安装IE7。有朋友在评论中反映我的Blog在IE7下打开时存在的问题：页底部分飘上来，挡住了第一篇文章的内容。

今天用IE7试了一下，果然如此。于是在网上查了查关于IE7对页面布局的影响，发现问题果然出在典型的“width/height误用”上。刚开始试着去掉了div的height属性，发现IE7/6倒是正常了，可Firefox反倒不显示“background”属性指定的背景图片了，真是怪哉……

在网上几经周折，终于找到了一个可以兼顾Firefox和IE的解决方案：用“min-height”替代原来的“height”属性。

最后，感谢崇尚环保主义精神的IE7 Standalone：<a href="http://tredosoft.com/IE7_standalone/" title="IE7 Standalone" target="_blank">http://tredosoft.com/IE7_standalone/</a>