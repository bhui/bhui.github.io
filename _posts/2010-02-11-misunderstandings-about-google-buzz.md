---
id: 863
title: Google Buzz的解读误区
date: 2010-02-11T23:40:24+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=863
permalink: /2010/02/11/misunderstandings-about-google-buzz/
dsq_thread_id:
  - "250428317"
  - "250428317"
categories:
  - Misc
tags:
  - Buzz
  - FriendFeed
  - Google
  - Salmon
  - Social
  - Twitter
---
Google发布Buzz后，网络上迅速出现了大量对Buzz的评论，有正面的，有负面的，有炒作概念的，有跟着起哄的，甚至引发了大家对Gmail安全的担忧。这其中不乏一些对Buzz的误读，所以，在这里以我个人的理解来解释一下。

**“Google Buzz是Twitter杀手！”**

这是大多数媒体最喜欢的炒作方式，又一个Killer App出现了，于是编辑们都兴奋了，又可以赚足眼球了。事实上，Google Buzz和Twitter总体来看并不是一个层面上的应用，还构不成真正意义上的Killer。一些冷静的分析还是看的比较清楚，Google Buzz其实主要针对的是[FriendFeed](http://friendfeed.com/)，因为它们都是聚合平台，让不同源头的信息聚合在一起。Buzz相对于FriendFeed的最大进步在于，它除了聚合信息之外，还创造性的利用[Social Graph](http://code.google.com/apis/socialgraph/)来聚合人际关系。

当然，Google Buzz除了聚合功能外，自身也充当了一个简单的信息源，可以在Buzz上发表富媒体信息。但事实上，你有自己充分的选择权，完全可以保持原有的习惯，在WordPress上写Blog，在Twitter上唠叨几句，这些信息最终都会自动被汇总到Buzz中来。

**“我们不需要又一个社交网络”**

当你迫不及待的跑来Buzz上兴奋的吼了几句后，才意识到它和Twitter也没多少差，反而在这里找不到Twitter上那种“振臂一呼，Follower百应”的成就感了。没过多久，你就会逐渐淡忘掉Buzz。这是因为，你把Buzz当成了一个和Twitter、Facebook、MySpace一样的社交网络。[“又一个新的SNS，我不得不又一次花费时间从头建立我的关系网络。”](http://code.google.com/apis/socialgraph/)其实这不奇怪，不光是你，连[Microsoft也这么认为](http://techcrunch.com/2010/02/09/microsoft-slams-google-buzz/)。

本质上，Buzz并不想打造一个新的社交网络，恰恰相反，它的目的是推进一系列开放标准，使用户不必在各个SNS维护一个又一个彼此独立的关系网络，使人际关系得以重用和汇聚，进而构造起一个去中心化的Social Graph，不依附于某一个特定的SNS。

Buzz倡导运用[XHTML Friends Network](http://gmpg.org/xfn/) (XFN) 和 [Friend of a Friend](http://www.foaf-project.org/) (FOAF) 挖掘和汇聚用户既有的关系网，实现SNS间的互操作性。如果各个开放SNS都能响应这一号召的话，那么将来我们就再也不用担心自己的人际关系被锁死在某个SNS中，甚至还可以借助新的SNS发现原有SNS中漏掉的好友。

**“Buzz让信息的回复和评论更加破碎了”**

这一点确实是目前不争的事实，因为无论你从Twitter往Buzz同步也好，还是打算反过来从Buzz发布到Twitter，你都得面对一个问题，回复和评论的不同步。你很可能因为只在Twitter上读消息而遗漏了Buzz里别人的评论，或许在习惯了Buzz后，又冷落了Twitter上的Followers。在Web应用越来越多的引入“聚合（Aggregation）”功能后，这个问题逐渐凸显出来。Google Buzz现在没有解决这个问题，但这只是因为目前的Buzz还尚不完整。[Buzz的API文档中有一节“Coming Soon”](http://code.google.com/apis/buzz/documentation/#coming-soon)，其中提到了Buzz未来对这一问题的解决之道——[Salmon](http://www.salmon-protocol.org/)。

之所以现在没有推出Salmon支持，我猜想，一方面是由于这个规范尚处在Draft阶段，另一方面它无法从Google单方面实现，因为信息源和聚合者都必须遵从Salmon协议，才能完整的实现评论同步。这个事情倘若让任何一家其它互联网公司来推，可能都收效甚微，但由Google Buzz倡导，其影响力就不可同日而语了。因此，Google在完成Salmon的支持前，先放出Roadmap来，让大家都意识到Google开放的心态和坚定的决心，这样Salmon才有机会得到广泛的认可和支持。

所以，就如同[Wave对大多数人来说也不过尔尔](http://blog.oasisfeng.com/2009/10/12/the-strategy-vision-behind-google-wave/)，只有当你透过API去洞察其背后所希望表达的真正意图后，才能深刻理解Google每一款产品的前瞻和愿景。在大多数人被Buzz的优雅与便捷所打动时，我更看重的是它将对整个SNS生态圈所产生的深远影响，和它在推动开放和标准化上的显著贡献。