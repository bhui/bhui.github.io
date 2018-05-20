---
id: 192
title: WordPress 2.1 is finally released!
date: 2007-01-24T01:13:18+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/01/24/wordpress-21-ella/
permalink: /2007/01/24/wordpress-21-ella/
dsq_thread_id:
  - "250426832"
  - "250426832"
categories:
  - Internet
tags:
  - AJAX
  - WordPress
---
这是WordPress的一次重大升级，终于实现了很多我等期待依旧的特性！更多激动人心的更新见下。要不是因为地震的网速后遗症尚未消除，我真的等不及DreamHost升级其One-Click Bot就想体验WordPress Ella了 ~.~

更新介绍就懒得自己翻译，直接转了“[总而言之,统而言之](http://jiangzhanyong.com/2007/01/wordpress-21-ella-187.html)”的帖子（纠正了几处翻译错误）：
  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

WordPress 2.1 版正式发行了，很让人兴奋。以下介绍原文来自 WordPress.org 网站，将原文主要内容简单翻译，仅作参考，部分关键词汇保留英文，以防翻错。如果网友发现其他错误，敬请指出，谢谢！

作为 WordPress.org 社区委员会、贡献者和志愿者的代表，我很自豪地宣布 WordPress 2.1 “Ella” 可以下载了。这个版本以爵士歌手 Ella Fitzgerald 的名字命名。以下是新版本的更新内容：

    *** 自动保存(Autosave) 能让你永远不会丢失一篇文章。
      
* 新的标签化编辑器(tabbed editor)允许你在写文章的时候自由切换所见即所得(WYSIWYG)和代码编辑两种方式。
      
* 无损的XML导入导出(lossless XML import and export)让你在不同的Wordpress blog之间迁移你的内容更加简便。**
  
<!--more--> * 我们完全重做的可视化编辑器现在还包括拼写检查(spell checking)功能。


      
* 新的搜索引擎隐私选项允许你设定自己的 blog 是否被类似 Google 的搜索索引。
      
* 你可以设置任何”页面(page)”来做你的站点的首页，并且将你最新的博文放在其他地方。这可以更方便地把 WordPress 当作内容管理系统(CMS)来用。
      
* 更有效的数据库代码，比先前版本运行更快。来自 MySQL 的 Domas Mituzas 仔细检查梳理了我们的全部队列代码。
      
* blogroll中的链接，现在支持子类，你闲的时候可以添加分类。
      
* 重新设计了登陆对话框。
  
    *** 更多的 AJAX 使得自定义项，修改，删除等更加快捷。我最喜欢的是评论页，可以让你随时批准或否决评论。**
      
* 页面(Page)也可以保存为草稿或私有了。
      
* 管理面板也更新了，可以更快地导入内容，看起来也更协调。
      
* 可以直接在控制台生成Rss feed，也可在背地异步生成。
      
* 评论Feed 可以包括所有的评论，而不再是最多10条。
      
* 提供更好的国际化方式，支持从右到左的语言。
      
* 上传管理器(upload manager) 让你轻松管理上传的图片，视频和音频。
  
    *** 捆绑了新版本的 Akismet 插件(译者注：反垃圾留言插件)。**

…等等等。还有很多金蛋隐藏起来了，找出所有新性能的最好办法是来进行试用。

【面向开发者的改进】

开发者将会特别喜欢这个发行，因为它有比 2.0版清晰的代码，包括了数以百计的增强，使得可以开发更为丰富的插件。以下是部分新的特点：

    *** 伪-cron(Psuedo-cron) 函数让你像 cron 一样安排更多的事件日程。**
      
* 用户管理可以更加舒适地管理成千的用户。
      
* 新的 WP_Error 类清楚地指出我们错误以及如何处理。
      
* Javascript 装载器(javascript loader)使得开发功能丰富的插件更为容易。
      
* 成吨的钩子函数(hooks)和接口函数(API)。
      
* 我们已开始完善我们的代码内置文档(fill out our code inline documentation)。
  
    *** 图像和缩略图的API(Image and thumbnail API)可于丰富媒体插件。**
      
* 自定义页头，颜色拾取器和图片处理裁切框架(image cropping framework)。

2.1 版本还包括550个bug 修正。

【WordPress的未来】

对我而言最令我兴奋的就是未来将会怎样。首先，2.0 版本系列已经获得了巨大的成功，超过180万的下载量，这里要感谢 Mark Jaquith 的工作，我们委托他维护稳定安全和2.0系列的 bug 修正到 2010年。

然而，对我们用户更为兴奋的事情，是我们新的开发周期。基于过去三年学到的开发 WordPress 的经验，我们决定像 Ubuntu 那样更加频繁进行更新，每年发行数个主要版本。那么，在 WordPress 历史上第一次，我可以告诉你下一个版本的发行日期：4月23号。并且更好的是，开发的动力来自你们对创意表中对新性能需求的投票。(但是等一下，还有一点：创意表现在采用新的 Hot-or-Not-like 界面进行投票，所以快来投票和发表你对 WordPress 2.2 版的看法。)

英文原文: http://wordpress.org/development/2007/01/ella-21/