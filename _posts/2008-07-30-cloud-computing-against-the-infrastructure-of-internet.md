---
id: 352
title: 云计算与互联网基础承载结构的矛盾
date: 2008-07-30T03:12:52+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=352
permalink: /2008/07/30/cloud-computing-against-the-infrastructure-of-internet/
dsq_thread_id:
  - "250427818"
  - "250427818"
categories:
  - Internet
tags:
  - Cloud Computing
  - Distributed
  - Telecom
---
今天听了电信领域战略专家刘南杰关于“互联网基因与电信发展”的一个主题讲座，了解到了一些从互联网最早期日子一路过来，在互联网公司和电信运营商之间那些貌合神离的微妙关系，以及在互联网经历爆发性增长后电信运营商所面临的转型压力。其中一个关于“云计算”的有趣话题引起了我的更多思索。

“云计算”这个词最近实在太热了，以至于只要是个互联网公司，要是还没有自己的“云战略”，那简直是抬不起头见人了。但是，云计算在承载了众多期望与理想的同时，是否真的是未来互联网服务的大趋势呢？云计算的未来究竟应该是怎样的形态？很遗憾，我也无法回答这些问题，但至少眼下，我们必须看到云计算所面临的现实问题。

<!--more-->众所周之，互联网的物理基础是由传统分组交换的语音承载网过渡而来的，即使是在向全IP演进的过程中，电信承载网络的结构也并没有发生本质的变化。这种结构是为传统电话业务而生的，它天然的符合语音依靠“虚电路”分组传输的需求。但是这种结构是否符合现今的互联网呢？答案是否定的。先让我们来看看电信承载网的结构到底是什么样的：（借用

[Wikipedia上的一副图片](http://en.wikipedia.org/wiki/Image:PSTN_office_classification_hierarchy.svg)）

<center>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2d/PSTN_office_classification_hierarchy.svg/400px-PSTN_office_classification_hierarchy.svg.png" alt="Telecommunication Network Hierarchy" />
</center>

可能在不少人的概念里，Internet是扁平的，是由大量网状分布的路由器汇聚起来的。这个理解从抽象层面是正确的，但在物理层面，传输网络实际是分层汇聚的。比如你从家里的ADSL访问Google.com，中间途径了运营商的接入网，城域交换网，骨干传输网，国际关口，骨干传输网，城域交换网，然后可能才到达Google的服务器。如果希望直观的了解这个过程，可以traceroute一下google.com，然后分别查询各跳IP的地理信息。

在地理拓扑上，电信网络是大致均匀分布的，这也是因语音呼叫的概率分布而决定的。假如我们能得到运营商的传统语音业务统计数据，然后铺开在地图上，我们可以看到一个大致均匀的分布（不考虑人口和经济发展的不平衡性），且所有节点的呼叫量基本是呈正态分布的。但是，互联网所展现的却是一幅完全不同的光景。倘若将互联网中涌动的数据流同样铺开在地图上，我们看到的是高度不均匀的分布状况。以Web服务为例，占全球不足0.01%的Web服务器却汇聚互联网80%以上的流量，而所有网络节点的流量呈幂次定律分布。这就是互联网的“无尺度性 (Scale-free)”。

<center>
  <img src="https://blog.oasisfeng.com/wp-content/uploads/2008/07/scalefree2.jpg" alt="Scale-free Network" title="scalefree2" width="480" />
</center>

它解释了为什么虽然电信运营商在不停的扩充其网络带宽，而我们也都在用宽带接入，但仍旧无法从很多主流互联网应用中体验到满意的速度，尤其是富媒体应用。比如国内的用户访问YouTube的速度就根本无法与访问本土视频网站相比，通常差了一个数量级。大量的数据汇聚到骨干传输网上，即使是拥有逼近TB级别传输速率的光纤网络也难以承受如此重负，尤其是在这个视频服务风行的年代，电信运营商早已叫苦不迭。

“云计算”的出现无疑更进一步的加剧了这种互联网流量的不均匀性。因为无论是Amazon的EC2还是Google的App Engine，都鼓励网络应用服务商商直接购买其提供的运算和存储能力，也就相当于租用Amazon或Google数据中心里的虚拟主机。倘若按照它们期望的趋势发展下去，互联网上更多的流量都最终汇聚到了少数巨型数据中心。在当前这个网络承载基础上，“云计算”真的能成为应用服务商和用户的双赢么？我看未必。除非现有的云计算能够向大规模分布式的方向演进。

<img src="https://blog.oasisfeng.com/wp-content/uploads/2008/07/classiccloud.jpg" alt="" title="Classic Cloud" width="478" height="425" class="aligncenter size-full wp-image-384" srcset="https://blog.oasisfeng.com/wp-content/uploads/2008/07/classiccloud.jpg 478w, https://blog.oasisfeng.com/wp-content/uploads/2008/07/classiccloud-300x267.jpg 300w" sizes="(max-width: 478px) 100vw, 478px" />

大规模分布式的“弥散云”是理想的，但在现实中实施起来却是困难的，即使大如Google这样的互联网企业，在全球也只能兴建为数不多的数据中心。对于分布在世界各个角落的用户，可能仍然不得不借助业已饱和的电信传输网络，在跨越众多中转节点后才能访问到最近的数据中心。其实，这个矛盾并非没有解决的对策，也不必对当前的电信基础网络作大规模的改造。问题在于，掌握着解决之道的人尚未真正意识到这一点，更没有找准自己的角色。虽然Google这样的互联网巨头在急不可耐的想要代劳，但事实上却显得力不从心。Google可以在互联网领域称霸，并不意味着它同样擅长其它领域。

反观如今全球的电信运营商，无不视互联网服务为新的战略增长点，纷纷大举进军传统互联网公司的领地。中国电信早在多年前就开始大力推广互联星空网络购物，而中国移动也将矛头直指竞争激烈的即时通信领域。可惜它们都希冀在一个自己所不擅长的领域内有所建树，却置自己真正的优势领域于不顾。试想，究竟是谁坐拥着遍布每一个城镇、通达每一个乡村的网络设施？这距离用户最后“1公里”的宝贵资源不正是令Google这些云计算倡导者垂涎欲滴的最彻底的分布式网络么？只可惜在习惯了以自己的意志主导各种电信服务并不断强加给用户之后，这些电信运营商，又怎能真正理解什么是互联网最需要的呢？

故步自封固然会彻底被互联网的高速发展所淘汰，转型是必须的，但如果看不清自己的定位，一味的去和互联网公司竞争又岂是电信运营商的出路所在？我相信，如果大型的电信运营商依靠长期积累而成的基础网络优势，通过适当延伸其网络设备的处理能力，用来提供类似Amazon EC2和Google App Engine的分布式云计算平台，甚至哪怕仅仅提供分布式存储服务，就足以发挥分布式云计算的真正优势，同时还可以大幅度缓解互联网高速发展所施加在电信主干承载网上的重负，一举两得，不是么？

<img src="https://blog.oasisfeng.com/wp-content/uploads/2008/07/dispersedcloud.jpg" alt="" title="Dispersed Cloud" width="495" height="427" class="aligncenter size-full wp-image-386" srcset="https://blog.oasisfeng.com/wp-content/uploads/2008/07/dispersedcloud.jpg 495w, https://blog.oasisfeng.com/wp-content/uploads/2008/07/dispersedcloud-300x259.jpg 300w" sizes="(max-width: 495px) 100vw, 495px" />