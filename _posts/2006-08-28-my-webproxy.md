---
id: 11
title: 自己搭建了一个WebProxy
date: 2006-08-28T14:40:00+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/08/28/%e8%87%aa%e5%b7%b1%e6%90%ad%e5%bb%ba%e4%ba%86%e4%b8%80%e4%b8%aawebproxy/'
permalink: /2006/08/28/my-webproxy/
dsq_thread_id:
  - "250425953"
  - "250425953"
categories:
  - Internet
  - Software
tags:
  - DreamHost
  - PHP
  - Web-Proxy
---
　　介于最近GFW活动越来越频繁，早先打开的Google News刚点一个链接就访问不了，脱机回退之后才发现原来上面出现了一则引述台湾媒体的新闻…… 实在是佩服GFW的处理效率啊！ 考虑到[新近购入的DreamHost虚拟主机](http://oasisfeng.blogspot.com/2006/08/blog-post_25.html)流量基本还未利用起来，于是决定搭建一个WebProxy，至少还可以访问一下Google Cache、Wikipedia吧。

<!--more-->　　

**（注意：因为自己搭建的WebProxy流量是算在你的虚拟主机IP上的，所以请不要随意用它访问GFW所不欢迎的网页，免得届时不仅自己的网站遭殃，还可能牵扯到不少同主机的国内用户。所以，请慎之！）**在选择相应的服务器软件时，倒是费了不少周折，先后尝试了多款开源的php版的WebProxy，效果都不理想。它们大多不能很好的处理隐式的链接，若遇上Ajax就更是一塌糊涂，不仅如此，还常常在引用script、CSS等环节上出问题。毕竟，这些开源的小项目都很少能有复杂的分析引擎。

无意中，我发现了一款比较另类的软件——[PHP Proxy](http://idea.hosting.lv/a/phpproxy/)（注意哦，此PHP Proxy非彼PHP Proxy，找到前者还真花了我不少功夫），它完全采取了与目前的WebProxy所不同的机理：服务器端（php）＋客户端（Python）。安装好服务器上的php程序（仅一个文件）后，在自己的客户端启动一个Python小程序后就创建了一个本地的中转代理。只需在IE中设置代理为localhost及已配置的端口，即与使用普通HTTP Proxy全无差别了。（或许应该称其之为Web HTTP Proxy吧）

绕开了WebProxy一般所必须面对的地址转换处理后，则所有的问题都不复存在了。试用了一阵子，完全和普通HTTP一样的稳定和方便，而且访问很多外国网站的速度都有明显提升。（嘿嘿，就我一个人使用的Proxy当然快了^_^） 注：因为前面提到的原因及带宽方面的因素，很抱歉这个WebProxy不能对大家开放试用。

附：[PHP Proxy](http://blog.oasisfeng.com/wp-content/uploads/2007/11/phpproxy-06.zip "PHP Proxy")（由于作者的主页已经无法访问，所以在本地放了一份供大家下载）。