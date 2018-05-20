---
id: 823
title: 从胶水到运河——Google Wave的战略使命
date: 2009-10-12T20:33:06+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=823
permalink: /2009/10/12/the-strategy-vision-behind-google-wave/
dsq_thread_id:
  - "250428313"
  - "250428313"
categories:
  - Internet
  - Thinking
tags:
  - API
  - Gadget
  - Google
  - Robot
  - Wave
  - Web 2.0
---
　　先来看一下Google的愿景及其诞生至今的战略布局。Google的终极愿景很明确，也几乎没有改变过，那就是：[“整合全球信息，使人人皆可访问并从中受益。”](http://www.google.cn/intl/zh-CN/corporate/) 这句话讲的挺有技巧，整合全球信息，并非简单的供你们搜索和访问，“从中受益”，那前提是Google需要充分从这些信息中挖掘出价值，而后才能造福大众。**“掌握和控制信息”是Google所有从属战略的核心。**

　　**第一代搜索引擎所代表的是“整合互联网静态信息”的愿景**，Google借助其强大的搜索引擎和海量存储成功的树立了搜索领域的霸主地位。在这个年代，整合互联网信息的方式相对比较直接了当，那就是“蜘蛛+索引+搜索”。大部分静态内容都是可以方便的直接访问到的，因此Google只需要构建一个巨型索引就可以达到整合信息的战略目的了。

<!--more-->　　伴随着Web 2.0的迅速发展，互联网的主要构成已经由静态信息向用户贡献内容倾斜。越来越多的网站主要依靠用户发表或上传的内容主导，Google也因时而动的推出了一系列针对性的垂直搜索，例如Blog Search、Groups Search、Photo (Images) Search、Code Search。但是，Web 2.0的一个显著特征是社会化，这就造成为数不少的用户贡献信息并不面对搜索引擎的蜘蛛开放，尤其是各大SNS社区，几乎都主动屏蔽了搜索引擎。出于用户隐私的保护，其它信息形式，如照片、代码等往往也部分性的不开放给搜索引擎访问。另一方面，Web 2.0提供了更为结构化的信息，这些信息依靠蜘蛛的抓取很难保留其结构化的原貌。不断涌现的新情况让Google觉得相当的被动，于是它启动了一轮庞大的

**“信息控制战”**，通过免费向用户提供有竞争力的各种信息的存储服务，达到将全球信息掌控在自己手中的目的。于是Gmail、Blogger、Picasa Web、Google Code便应运而生。但凡有其它初创型公司挡在了Google的战略大道上，便不客气的一口吞掉，比如YouTube、Writely。在如此强势的战略夹击下，Google在Web 2.0的时代勉强保持住了它在信息整合方面的优势地位，但**面对Facebook、Twitter等新兴信息承载形式的崛起，却显得颇有些步履蹒跚、力不从心了**。

　　在后Web 2.0时代，互联网对于大众的意义，已经逐渐从一个单纯的信息获取通道，转变为一个全能的服务平台，这在最近刚刚被提出的Gov 2.0中体现的尤为明显。交互应用开始取代信息媒体，成为互联网的主导力量，并剧烈的改变着互联网的面貌。尽管Google一直致力于推动数据开放化和API标准化，但互联网毕竟不是一家说了算，长尾的延伸，让Google执行其战略愿景的难度越来越大。**搜索引擎的历史局限性注定其难以在新的互联网格局下继续担当整合全球信息的重任。**首先，搜索只能控制用户在互联网行为的最初阶段，其快速的逸出性使搜索引擎很难像SNS那样掌握更丰富的用户信息；其次，交互应用取代单纯的信息呈现后，已经不再可能简单的通过搜索引擎体现其对用户的价值；最后，应用之间的Mashup使得互联网上信息的拓扑层次愈加复杂，搜索引擎扁平的索引方式已经很难有效整合这些信息。

　　在这样一个大背景下，Google开始酝酿其夺回战略主动权的新型武器，这就是Google Wave。表面上，如同Google所声称的那样，“Google Wave is an online communication and collaboration tool that makes real-time interactions more seamless &#8212; in one place, you can communicate and collaborate using richly formatted text, photos, videos, maps, and more.” Google当然不会直接告诉你Wave背后的战略意图，但无论是从开发资源投入、系统复杂程度、宣传推广攻势上，Wave都是空前的。其邀请机制的苛刻程度甚至超过了当年的Gmail（后者如今以成为Google除搜索外最引以为自豪的产品）。这些都充分显示出Google对于这款产品的重视程度。

　　**其实，Wave API才是揭开Google Wave战略的关键。**为什么Wave的Preview邀请明显倾向于开发者和合作伙伴？在Wave主体功能都尚未完成时，各类API和SDK却得到了优先的完善。显然，Google向第三方开发者频频伸出橄榄枝并不会单纯因为它同时提供API接口这么简单。下面就来细细解剖一下Wave API，看看这葫芦里究竟卖的什么药。

　　Wave API目前分为两个大类：Extension和Embed，前者相当于插件，为Wave扩充功能；后者相当于呈现包装，可以将Wave嵌入其它现有应用中。Embed的作用不用我多作解释了，而**Extension则是Wave的战略核心**。

　　Extension又可分为两个分支——Robot和Gadget，它们与Wave一起构成了应用开发中典型的MVC架构：Model是Wave框架本身，View是Gadget，而Controller则是Robot。Wave本身的三层数据结构（Wave-Wavelet-Blip），具有动态性、实时性、可交互性的特点，迎合互联网应用的Model设计需求。Gadget作为Rich Text等标准媒体类型之外的扩展接口，使Wave可以适用于各种特殊应用场合。而Robot则依应用形式的不同，可充当不同的具体角色：在封闭的Wave应用中，它们充当传统的Controller角色；而在Mashup的应用中，Robot则充当胶水，可以是Importer、Exporter或者是Transformer。

　　Wave API的一些设计理念也从一些侧面折射出Wave的战略愿景，比如：

  * **Robot也可以创建它的Private Wavelet，或者与其它Robot共享Wavelet。**这些Wavelets对用户是不可见的，它们可以被用作Robot的持久存储，或是通信通道。
  * **不可见Wavelet可以看成是一个支持事件通知的“通信通道”，其中的Blip则是单个“消息”。**这给应用开发提供了充分的发挥空间，比如用作类似于Unix下的管道，实现应用搭桥；或者用作Provider/Consumer模型的任务分发队列；又或者用于选择性的组播；甚至是可修改的全局参数集。
  * **可见的Wavelet则可以当作一个人机交互的接口，便于用户以一种类似对话和交互编辑的形式与应用进行交流**。当然，借助Gadget，还可以扩充至任何需要的交互形式。

　　虽然整合目前互联网上的众多应用并不现实，但Google鼓励开发者通过Extension将应用的功能和接口嵌入到Wave中来，即Google所设想的“All in one place”。表面上，Wave像胶水一样，可以方便的将实现了Wave Importer和Exporter的应用Mashup。不过，**当胶水成为事实上的标准之后，应用之间的竞争壁垒则被Google渐渐的填平。**到那时，Wave便升华为运河，而你无论是摆渡者，还是商人，都只是在这条河道上碌碌奔波的营生者，时刻担心被竞争对手取而代之，只有这条运河本身，才是无法被取代的垄断者。

* * *

　　还记得很久之前曾经读过一篇科幻小说，描绘了一个“互联网的幻境”：在那里有各式各样的智能零件，每个人可以充分发挥想象力组装出各种或实用或有趣的器具来装点自己的小屋，整个幻境世界的公共设施也是由术士们（开发者）自发协作建设起来的，而那些Geek们则喜欢利用系统的漏洞玩一些“黑魔法”。

　　透过Google Wave，我似乎依稀看到了“互联网幻境”的轮廓……