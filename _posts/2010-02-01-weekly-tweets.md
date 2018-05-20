---
id: 849
title: 【闲言碎语】淘宝电器城、网瘾战争、轩网、GAE、tb.ly、第一推动丛书……
date: 2010-02-01T00:00:37+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=849
permalink: /2010/02/01/weekly-tweets/
dsq_thread_id:
  - "250428333"
  - "250428333"
categories:
  - Thinking
tags:
  - Google
  - google app engine
  - Taobao
  - tb.ly
---
自从习惯了Twitter后，Blog写的是越来越少了。Twitter虽好，但相对于Blog，它其实很不利于内容的沉淀，再加上因国情问题而导致很多朋友无法访问，有价值的信息就此流失。为此，我准备尝试每周做一个Tweets的合辑，让这周中那些不是废话的内容能有机会沉淀下来，并且让更多人有机会从中获取有用的信息。当然，也随时欢迎在[Twitter上Follow我](http://twitter.com/oasisfeng)。

<!--more-->

**<span style="text-decoration: underline;"><em>Monday, 25th of January.</em></span>**

揭秘搜索引擎关键字过滤背后的实时审查系统 http://gfwrev.blogspot.com/2010/01/blog-post.html

淘宝电器城在走一个危险的模式，它通过集中展现抹杀店铺的个体品牌和特色服务，最终将竞争引向赤裸裸的价格战。淘宝上那些靠口碑经营所积累的店铺品牌，可能就此毁于一旦。

**<span style="text-decoration: underline;"><em>Tuesday, 26th of January.</em></span>**

Google Reader的新特性，Feed for any page: http://googlereader.blogspot.com/2010/01/follow-changes-to-any-website.html

看完了朋友推荐的《网瘾战争》，作为一个曾经的魔兽玩家，我能深切体会到这种对现实社会近乎绝望的悲愤呐喊。那一刻，我感动的忍不住落泪了……

**<span style="text-decoration: underline;"><em>Wednesday, 27th of January.</em></span>**

在Blog上有人留言说“我最近在重玩台服的軒網 那個轩网·异眼我找很久也找不到 請問可以給我嗎?” 一个网游能在关服数年后仍然拥有忠实的玩家，我想也只有轩辕剑网络版和WoW能做到吧……

RT @oasisfeng 网上看到有人说，研究增强Java的 Hot Swap就是一个dead end。难道最近苦无进展的我，也要陷进这个死胡同了……？//再感慨一下两个月前的感慨。当你以为攀上了顶峰时，却只看到一条被迷雾吞没的险道通往更高处……

不过我在攀登这座无尽之峰的山路中，沿途也收获了很多东西，一些将来无论踏足平川还是穿越激流时都能用得上的经验。

**<span style="text-decoration: underline;"><em>Thursday, 28th of January.</em></span>**

iPad大失所望，看来不用贱卖我的eBook了。

看来Google对自家Public DNS的短处也看的很清楚，并且在积极推动改善。 http://googlecode.blogspot.com/2010/01/proposal-to-extend-dns-protocol.html

原来Google App Engine已经悄悄支持泛域解析了！在GAE中配置域名，并在Apps里添加应用URL为\*，然后修改DNS配置，加一个\*的CNAME指向ghs.l.google.com.就可以使用任意二级域名访问GAE应用了。

目前真正可用的Google官方ghs只剩最后的一个幸存者了，如果你从某些渠道获得所谓的ghs IP，请务必小心，这些很可能只是一个反向代理（存在一定的安全隐患）。验明真身的方法是ping -a 这个IP，看域名是否隶属于1e100.net

**<span style="text-decoration: underline;"><em>Friday, 29th of January.</em></span>**

在新开张的Chromium-HTML5论坛上询问了Chrome支持Offline标准的计划，得到的答复是“It&#8217;s planned for Chrome 5. I think it&#8217;s going to ship in the next dev channel as well.”

估计差不多正好那时候可以完成tb.ly的HTML5离线功能的重构。

**<span style="text-decoration: underline;"><em>Saturday, 30th of January.</em></span>**

tb.ly开始测试二级域名跳转功能，淘宝店铺二级域名无需申请即可直接享受tb.ly同名二级域名。例如，输入nokia.tb.ly即可直接跳转至nokia.taobao.com。后续将推出基于店铺二级域名的店内商品专享短网址~

有别于tb.ly采用php编写的核心部分，目前的二级域名支持是用Google App Engine实现的，关于其中的实现细节以及GAE和php混搭的经验，我准备写一篇Blog来分享。

写完了这篇《在Google App Engine中使用泛域二级域名》，该吃饭去了。 http://blog.oasisfeng.com/2010/01/30/use-wildcard-domains-in-google-appengine/

http://www.squish.net/dnscheck/ 是我迄今为止见过的最为强大的DNS分析、检测工具。全路径解析跟踪对与诊断DNS记录的故障非常有帮助。

**<span style="text-decoration: underline;"><em>Sunday, 31st of January.</em></span>**

tb.ly为你提供超便捷的淘宝搜索：只需在浏览器地址栏输入“tb.ly?搜索关键字”即可带你直达搜索结果！现在就试试看： tb.ly?诺基亚E71

阔别十余年后，我又再次从浙江图书馆借来了这两本第一推动丛书中的《夸克与美洲豹》和《宇宙的琴弦》。抚摸着泛黄的书页，又想起初中时每天放学后在书店蹭书读的我，双腿站的发麻了都浑然不觉。

当年正是这套《第一推动丛书》让我一头扎进了科学的殿堂。前两个系列中的经典，我省吃俭用只买了《时间之箭》和《皇帝新脑》，其它很多本都是在书店蹭着读完的。后来许久没有关注，现在才知原来2004年又出了第三套。

Google开始在Docs和Sites服务中驱逐IE6！卸掉包袱，轻装上阵，只有做过前端的开发人员才能真切体会到Google这一决定背后的痛楚。http://is.gd/7pEQt

好消息呀~ Google Apps Script终于开放给标准版用户了！现在免费用户也可以用Server-Side JavaScript给Google Docs编写高度自由的扩展功能了！真是让人不禁浮想联翩~ http://is.gd/7pGBA

第一个想到的就是给我们的小饭桌账本(Google Spreadsheet)增加一个欠费提醒功能。哈哈哈~

Google Maps新版S60客户端的地标同步功能太方便了！今晚去普罗旺斯吃饭时就事先star了一下地标，从浙图出来直接打开Maps就找到地儿了~ 终于不用再很傻逼的从Google Maps里导出地标为Nokia格式，再传入手机了。

我现在用Live日历作为Google Calendar的桌面端呈现（这个还真有点讽刺……），不知各位推友是否有更方便易用的客户端推荐呢？