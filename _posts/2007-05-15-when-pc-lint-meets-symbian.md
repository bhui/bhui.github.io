---
id: 242
title: 当PC-Lint遇上Symbian
date: 2007-05-15T00:17:23+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/05/15/when-pc-lint-meets-symbian/
permalink: /2007/05/15/when-pc-lint-meets-symbian/
dsq_thread_id:
  - "250427296"
  - "250427296"
categories:
  - Development
  - Symbian
tags:
  - C
  - EPOC
  - PC-Lint
  - Symbian
  - TRAP
---
<a href="http://www.gimpel.com/html/pcl.htm" target="_blank">PC-Lint</a>是一款强大的C/C++程序检查工具，毫不夸张地说，如果编译器能为你发现20%的程序缺陷，那么PC-Lint至少还能为你发现余下的65%。（最后15%还是留给你自己去排查吧，机器始终是无法取代人脑的~）

可是，当PC-Lint遇上Symbian，就像那法力无边的如来佛遇上了刁钻难缠的孙悟空，也常常拿它没有办法。如今咱可是和谐社会了，怎么说也不能一怒之下就将孙猴儿打下五指山，落的个百年不得翻身吧。为了让两位大爷和平共处，我这观世音也只好费力的来调解调解了。

首先，在下面的地址取得Symbian官方提供的Lint配置文件：
  
 <a href="http://www.symbian.com/developer/techlib/v9.2docs/doc_source/faqsdk/faq_0449.html" target="_blank">http://www.symbian.com/developer/techlib/v9.2docs/doc_source/faqsdk/faq_0449.html</a>
  
（如果官方的链接无法下载，请[[点击这里]](http://blog.oasisfeng.com/wp-content/uploads/2007/05/epoc.zip "PC-Lint Configuration for Symbian")下载其副本）

借助官方的配置文件，PC-Lint已经能够识别大部分的Symbian程序代码。但实践中遇到的一些Lint提示仍然是这份97年之后再也没更新过的配置文件所能应付的。在这里，我补充一些自己总结的额外规则，提供给大家参考：

<pre>-D_UNICODE

-e1774			// Disable dynamic_cast
-emacro(717, *)		// Ignore do{...} while(0) in macros
-emacro(???, _LIT)
-emacro(???, _L)
-function( exit, User::Leave, User::LeaveNoMemory )
-function( __assert, User::LeaveIfError )</pre>

至于TRAP/TRAPD所产生的“Warning 655”，始终未能找到有效的消除方法。（当然，最坏的情况下你也可以加上括号以迁就PC-Lint的智商……）