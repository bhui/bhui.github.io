---
id: 296
title: 初步完成Position Provider接口的反向工程
date: 2007-12-18T22:49:19+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/12/18/reverse-engineered-nokia-s60-position-provider-interface/
permalink: /2007/12/18/reverse-engineered-nokia-s60-position-provider-interface/
dsq_thread_id:
  - "250427636"
  - "250427636"
categories:
  - Development
  - Symbian
tags:
  - LBS
  - Nokia
  - Position
  - S60
  - S60v3
  - Symbian
  - UIQ
---
经过两周业余时间的努力，终于初步完成了S60 3rd FP1中Position Provider接口(EPos Plug-in Framework)的反向工程（主要是CPositioner及相关类），并成功在模拟器上将测试第一个Demo Plug-in通过。

说起这个Position Framework，还真有点耐人寻味。<!--more-->它最初出现在Nokia S60 3rd MR SDK中，LBS系列头文件的署名是Nokia Corporation，而同一时期同样基于Symbian 9.1的UIQ3中却没有这个看到它的身影，由此推测这似乎是Nokia在Symbian OS之外独立开发的组件。但在后来基于Symbian 9.2的UIQ3.1中，出现了几乎与S60相同的LBS系列头文件，署名却意外的变成了Symbian Ltd.。这里所说的“几乎相同”是拿同期的S60 3rd FP1相比较的，在LBS系列头文件看似完全一致的同时，却出现了一些无法掩盖的裂隙——双方对同一常数定义了不同的数值，比如KPositionMaxModuleName，其结果直接导致TPositionModuleInfo类的大小和成员偏移不同，这也就意味着为两个平台所开发的LBS应用将可能是二进制不兼容的（好在源代码级别仍然兼容）。其中的种种因由我就不便在这里作过多揣测了。

虽然同样提供了Location Based Service面向应用的接口，但由于UIQ阵营尚无一款内置GPS的手机上市（Moto Z8号称将于本月底上市），加上UIQ Developer社区在LBS接口使用中所反馈出来的种种缺失问题，让我们很难将其与Nokia S60 3rd相提并论。反观后者，SDK中除应用层接口外，Server端的EPos系列组件从S60 3rd MR开始就存在了，而且在早期的内置GPS手机型号中表现良好。

到Position Provider接口上来，Nokia虽然提供了完整的组件，但在对待开发者社区的态度上却比UIQ小气多了。不仅UDEB下的文件其实是Release编译（UIQ人家至少还是标准的Debug编译），而且大量的系统接口被以Partner/Internal的名义隐藏起来，没有头文件不说，甚至连.lib及target的.dll都被斩草除根，丝毫不给独立开发者以使用机会。那么Nokia做的这么绝的目的又何在呢？大家不妨到<a href="https://pro.forum.nokia.com/productList.do" target="_blank">它的eStore</a>上看看就清楚了，<a href="https://pro.forum.nokia.com/showProduct.do?product_id=2420" title="&lid=Partnering+API+Request+link" class="swhitebg_link" name="&lid=Partnering+API+Request+link">Partnering API Request</a>可是上架出售的商品，光是这个Request Ticket就得花160欧元。（而且按照商品描述，如果Request被拒，不保证退还上述费用……#&%^!@）

对于一个独立 的免费软件开发者而言，从官方渠道获取这些接口无疑是难以承受的。所以我选择了“自力更生”，虽然Nokia已经尽可能的斩除了探索其内部接口的线索，不过它总无法阻挡无畏的开发者采用最极端的反向工程手段（呃，我也算是出于教育和研究目的吧，不涉及任何商业行为）。没有.h？自己写！没有.lib(.dso)？自己生成！找不到target版本的文件？无妨，现在已经有了<a href="http://www.symbaali.info/2007/10/exploring-s60-with-allfiles.html" target="_blank">Platform Security的破解方法</a>，从实机ROM中提取出来用就行了。打算最近写一篇教程，就叫做“[How to use unpublicized API in Symbian](http://blog.oasisfeng.com/2008/03/03/how-to-use-unpublicized-apis-in-symbian-2/)”吧，将这些经验分享给遇到同样困扰的朋友。