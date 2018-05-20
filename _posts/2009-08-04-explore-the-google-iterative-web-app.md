---
id: 780
title: 探究Google的Iterative Web App软件架构
date: 2009-08-04T23:00:42+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=780
permalink: /2009/08/04/explore-the-google-iterative-web-app/
dsq_thread_id:
  - "250428276"
  - "250428276"
categories:
  - Development
  - Internet
tags:
  - Architecture
  - Gmail
  - Google
  - Iterative
  - Labs
---
Google的软件架构向来是最吸引广大开发者的眼球并被人们乐此不彼的津津乐道，尤其是那些运作在Google最杰出服务背后的软件架构。

Google在2004年“愚人节”推出的Gmail服务可以说是Google众多服务中，除搜索外最杰出的典范之一。Gmail在过去五年多的时间里，也经历了一个持续发展和演进的过程。新功能的推出和用户体验的改善或许是大家谈的最多的，但其底层架构的变迁却并不常常能被用户切实感受到。其实，正是因为Gmail底层架构的不断升级，才支撑其众多新特性和功能的更快开发并上线。

早在2007年10月，Gmail的官方Blog上就曾经发表过一篇关于其架构变迁的文章“[Code changes to prepare Gmail for the future](http://gmailblog.blogspot.com/2007/10/code-changes-to-prepare-gmail-for.html)”，其中提到：
  
<!--more-->

> So recently the Gmail team has been working on a structural code change that we&#8217;ll be rolling out to Firefox 2 and IE 7 users over the coming weeks (with other browsers to follow). You won&#8217;t notice too many differences to start with, but **we&#8217;re using a new model that enables us to _iterate_ faster and share components&#8230;**

这里第一次公开提到了“Iterate”，表明在新的架构下，Gmail的开发团队开始以[迭代的敏捷开发模式](http://en.wikipedia.org/wiki/Iterative_and_incremental_development)进行着Gmail的维护和增量开发。

随后，在2008年5月，Gmail正式推出了一项让人耳目一新的功能，确切的是，是一系列新功能的入口——[“Gmail Labs”](http://gmailblog.blogspot.com/2008/06/introducing-gmail-labs.html)。这这里，你可以选择性的激活你所喜欢的新特性，关闭那些对你作用不大或者不好玩的功能。这说明，Gmail此时的底层架构已经过渡到了成熟的模块化和前后端高度整合的程度。“Gmail Labs”可以看作是一个基于模块化架构的“插件平台”，使得新功能和特性可以以插件的形式开发出来，并由用户决定其想要的组合。

在后来2009年3月中[Gmail官方Blog的一篇文章](http://gmailblog.blogspot.com/2009/03/gmail-labs-goes-global.html)进一步揭示了“Gmail Labs”的一些内幕：

> **Every time a Gmail user signs in we create a custom version of JavaScript for them based on the Labs features they have enabled.** Since we have 43 Labs right now, there are 243 (~8 trillion) possible versions of the Gmail JavaScript that a user could get. If you account for the 49 languages where Labs are now available, it gets even bigger &#8212; 49 x 243 (~430 trillion) versions. It would obviously be a challenge to actually test all of these versions. But we put a lot of effort into building an architecture that supports this type of modularity, and fortunately, it seems to be working pretty well so far. So we figured, why not, what&#8217;s another another 422 trillion permutations?

从中，我们可以看出一些线索：Gmail Labs的插件平台主要负责整合各项Labs插件对系统的改变，包括动态生成及组合影响前端界面呈现的Javascript，（可能）包括在基本处理流程的各环节中嵌入各插件的特殊处理逻辑，类似Filter Pattern。结合Google推出的开源前端框架GWT，猜想Gmail的前端界面渲染上也采取了类似GWT的“容器”+“控件推送”的机制。使得小特性的开发不需要分开完成前端和后端的设计，毕竟大部分Labs特性对前端界面的影响都在一个很有限的范围内，并以“调整”、“嵌入”等简单形式为主。

最近，Google Mobile似乎也走在了底层架构升级的浪尖。在他们[官方Blog的最近多篇文章](http://www.google.com/search?q=site%3Agooglemobile.blogspot.com+iterative+web+app)中，都显著的提到了“Iterative App”这个名词，并统一引用了下面一段话作为这个系列中每篇文章的开篇：

> On April 7th, we announced a new version of Gmail for mobile for iPhone and Android-powered devices. Among the improvements was a complete redesign of the web application&#8217;s underlying code which allows us to more rapidly develop and release new features that users have been asking for, as explained in our first post. We&#8217;d like to introduce **The Iterative Webapp**, a series where we will continue to release features for Gmail for mobile.

看来，Gmail for Mobile也吸纳了Gmail桌面版的经验，使用了可迭代开发的底层架构。随后，我们也可以看到，Gmail for Mobile的新特性推出速度确实加快了很多。

综合上面的各种线索，我们不难得出，Google所谓的Iterative Web App，指的是一种对敏捷迭代开发有较高亲和力的软件架构。在传统的层次化、分布化、服务化、易治理的Web架构基础上，Google进一步的将项目管理的因素融入到软件架构之中，形成了一个依靠架构优势保障和推动敏捷开发的新模式，避免了迭代开发理论在项目实践中可能遇到的“空中楼阁”问题。

最后，总结一下“Iterative Web App”架构的几个典型特征：

  * 高度模块化和层次化的系统设计，尽可能节省增量开发或插件化开发的重复工作量，确保迭代开发的编码环节是真正“敏捷”的。
  * 高度服务化的系统布局，确保核心数据和功能独立于繁复的特性之外稳定发展。在不断推出新特性并改善现有功能的同时维持核心功能的稳定可靠。
  * 灵活可控的特性容器（平台），支撑多样化的特性开发，并充分隔离各种特性间的相互影响，同时也为敏捷开发的并行性提供可能。
  * 模块化测试和集成测试相结合的测试框架，保障迭代开发模块的完备性和系统的整体可用性。
  * 自动化的部署系统，保障迭代开发的新特性和功能增强可以迅速可控（分阶段、可定制化……）的部署到线上。