---
id: 251
title: 虚拟主机新一轮性价比之王：Site5
date: 2007-06-10T23:27:47+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/06/10/site-5-overview/
permalink: /2007/06/10/site-5-overview/
dsq_thread_id:
  - "250427383"
  - "250427383"
categories:
  - Internet
tags:
  - BlueHost
  - DreamHost
  - HostGator
  - HostMonster
  - Site5
  - SSH
  - SSL
---
最近Dreamhost老是出问题，竟然出现一天之内连续4次当机，实在让人莫名火起。最近一个月的Siteuptime统计显示在线时间已经跌倒了99.5%左右。本来都差不多打算继续次年续费的了，看来不得不重作考虑。

Dreamhost首年$22.4的优惠价确实吸引了不少客户，但一年之后面对不菲的续费价格，就不得不开始慎重考虑各种综合因素了。受Dreamhost上述状况的影响，我首先考虑的因素就是可靠性保证，目前不少专业的虚拟主机供应商都明确提出了99.9%的“在线时间保证（Uptime Guarantee）”，所以我首先基于这一条件作了第一轮海选。
  
<!--more-->


  
其次，由于这一年来着实被Dreamhost给惯坏了，有事没事就喜欢登录SSH上去折腾，装软件也懒得用FTP，直接wget省事儿，甚至于已经习惯于拿它的SSH Tunnel当Socks5代理来穿越ＧFＷ。因此，倘若离开了SSH，我可能还真不能忍受那种倒退了。（再说，国外的虚拟主机用FTP连接本来就慢……）这么一来，便没剩下几家符合条件的候选者了：

<p align="left">
  <a href="http://www.bluehost.com/track/oasisfeng/blog" target="_blank">BlueHost</a>、<a href="http://www.hostmonster.com/track/oasisfeng/blog" target="_blank">HostMonster</a>、<a href="http://secure.hostgator.com/cgi-bin/affiliates/clickthru.cgi?id=oasisfeng" target="_blank">HostGator</a>、<a href="http://www.site5.com/in.php?id=37105-15" target="_blank">Site5</a>
</p>

除了Site5，前面三家公司在国内的相关网站和论坛上介绍的比较多，也都有不俗的表现，实在难以取舍。因为BlueHost和HostMonster系出同门，所以在参数和功能上都相当接近。而HostGator虽然赞扬的声音不如它们，但从实际Host的网站数量来看，却丝毫不逊色。（你会发现好几个热门的虚拟主机比较和推介网站，比如<a href="http://www.idcspy.com" target="_blank">www.idcspy.com</a>都是Host by HostGator，这比Review可要有份量的多）。

本来HostMonstor是当之无愧的性价比之王，但自从今年涨价之后就远不如从前那么吸引人了。直到我发现了Site5，才终于找到了新一轮的性价比之王！在 **$5/月*** 这样极具诱惑的价格下，让我们来看看Site5还有什么独到之处呢：（那些“大众化”的特性这里就免去不提了）

<p style="text-align: center">
  <a href="http://www.site5.com/in.php?id=37105-15"><img src="https://www.site5.com/creative/2db/banner1.gif" dragover="true" alt="Site5 $5 Hosting Deal" border="0" /></a>
</p>

<li dragover="true">
  <strong>110G空间、5T/月的带宽</strong>：这个比例较之大部分的主机提供商来说都更为合理。毕竟带宽是浮动而且常常难于预料的，而空间则可以明明白白的计划使用。
</li>
<li dragover="true">
  <strong>独立IP地址</strong>：莫要小看这一点，在虚拟主机供应商中，鲜有在平民级方案中提供独立IP的，比如Dreamhost的独立IP就是额外的增值服务，另行计费且不算便宜。IX Web Hosting也正是依靠其独立IP作为卖点笼络了不少客户。说的简单一点，独立IP可以最大程度免除国外虚拟主机的一个重大隐忧——“被盾”，从而不必日夜忧心与你共用虚拟主机的用户在提供什么内容。
</li>
<li dragover="true">
  <strong>SSL</strong>：提供电子商务的必备条件，同时也是实现安全PHP Proxy穿梭的前提。加上独立的IP地址，你可以提供完全自主的SSL服务，而不同于大部分虚拟主机服务商所实现的“Shared SSL”。
</li>
<li dragover="true">
  <strong>快速安装超过50种常用服务</strong>：这一点上要比Dreamhost大气多了，当然明显也是通过Fantastico提供的支持。
</li>

<p dragover="true">
  从我这几天来所了解的这么多虚拟主机供应商中，还真找不出别家同时提供“SSH”、“独立IP”和“SSL”功能的。
</p>

<p dragover="true">
  上面这些强大的功能惶且不论，Site5还有一个独立无二的特性——“多帐户独立管理（Multi-Site）”。用过Dreamhost的朋友可能还不一定了解其Web帐号授权功能，对于合租虚拟主机服务的用户来说，这一功能可说是非常重要（这也是众多合租团体都倾向于选择Dreamhost的重要原因）。它可以让你为多个合租者分别启用独立的管理帐号，分别管理各自的域名、Email、网站参数等，避免了单一管理的麻烦和安全隐患。而Site5所提供的“Multi-Site”则将此功能更加完美的演绎出来，甚至每一个用户都可以拥有完全等同的后台管理界面，就如同独立申请的虚拟主机一般无异，而彼此之间不能看到他人的帐号设置，充分保障了合租个体的利益和安全！更Cool的是，多个用户帐号之间可以精确调节资源的分配比例，比如空间、带宽、Email等，并由系统自动保证限额不被超出。
</p>

Site5目前提供了两种“Multi-Site”方案，配合当前正在开展的[限量“二折优惠（80%-off）”计划](http://www.site5.com/specials/)，只需比上述普通方案多出“$1.2/月*”即可支持6用户的独立管理，

从功能和指标来看，Site5给人留下了深刻的印象。不过像虚拟主机这种东西还是要用过了才能体会好坏，目前所能见到的国内评论不多而且大有枪文的感觉，期待有在国内的朋友使用过Site5服务来分享一下使用感受。

<small>注：上述价格都适用于预付两年。</small>