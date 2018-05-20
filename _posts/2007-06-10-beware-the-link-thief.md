---
id: 249
title: 时刻警惕盗链的威胁
date: 2007-06-10T00:34:05+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/06/10/beware-the-link-thief/
permalink: /2007/06/10/beware-the-link-thief/
dsq_thread_id:
  - "250427366"
  - "250427366"
categories:
  - Internet
tags:
  - Bandwidth
  - DreamHost
  - MP3
  - 盗链
---
今天在查看主机的流量统计数据时，惊奇的发现从5月28日以来，Blog流量呈高速攀升之势，在这两天已达到峰值，日均流量竟然几逾1G！

<p dragover="true">
  难道是近日的话题中有什么敏感内容，以致招来大量访客？结果显然不是这样。从日志分析中的“Referring Site Report”来看，music.soso.com这个站点占据了绝对主要的流量，而打开log一看，其中已经完全被下面这样的记录所充塞：
</p>

<p dragover="true">
  58.16.118.29 &#8211; &#8211; [09/Jun/2007:00:09:00 -0700] &#8220;GET /wp-content/uploads/2006/09/24hrs.mp3 HTTP/1.1&#8221; 206 69155 &#8220;http://music.soso.com/q?w=94001592c7fa3b44&sc=mus&ch=w.q&sip=202.108.4.105&sport=3118&ty=14&songname=xc8xe7xb9xfbxc3xbbxd3xd0xc4xe3&size=6.6M&sig=xc4xaaxcexc4xcexb5&clz=mp3&#8221; &#8220;Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)&#8221;
</p>

<p dragover="true">
  <img src="https://blog.oasisfeng.com/wp-content/uploads/2007/06/refsite.png" alt="Referring Site Report" />
</p>

原来是因为去年8月的一篇Blog，介绍了Google MP3 Player的保护原理：

<a href="http://blog.oasisfeng.com/2006/08/24/always-show-google-media-player/" target="_blank">http://blog.oasisfeng.com/2006/08/24/always-show-google-media-player/</a>

没想到其中用EMBED标签引用的MP3文件都被腾讯搜搜的MP3引擎给索引了，直接招致如此高的带宽消耗，还好有Dreamhost的海量带宽（2T/月）撑着，站点才不致被叫停……

由此可见，介于国内目前尚不成熟的网络道德，还是需要时刻警惕盗链的威胁。尤其应避免在网站上放置不加盗链保护的媒体文件。另外，养成常常留意日志的习惯也是非常重要的。 (: