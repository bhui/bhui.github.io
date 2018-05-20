---
id: 22
title: 路由器也能作虚拟主机？
date: 2006-08-22T14:14:00+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/08/22/%e8%b7%af%e7%94%b1%e5%99%a8%e4%b9%9f%e8%83%bd%e4%bd%9c%e8%99%9a%e6%8b%9f%e4%b8%bb%e6%9c%ba%ef%bc%9f/'
permalink: /2006/08/22/router-as-virtual-host/
dsq_thread_id:
  - "286357003"
  - "286357003"
categories:
  - Computer
  - Internet
tags:
  - ASUS
  - Linux
  - Router
  - Web-Server
  - Wireless
  - WL-700gE
---
Keywords: Wireless Router, Host Service, ASUS WL-700gE, Linux, Web Server

　　看来我又一次低估华硕的创意了！

　　还记得昨天提到的“[关机也能BT——华硕的无限创意](http://oasisfeng.blogspot.com/2006/08/bt.html)” ，这款产品特别的功能勾起了我的好奇心，今天在网上了解了一些详情后，发现原来它的功能还远不止“关机BT”那么单纯呢！

<!--more-->　　参见硅谷动力所作的评测：

<http://www.enet.com.cn/article/2006/0217/A20060217502575.shtml>

　　其中提到的有一点功能引起了我的很大兴趣：**HTTP/FTP Server**。是否意味着用它作路由器就可以代替电脑长期开机“兼职”虚拟主机呢！毕竟很少有人愿意将自己的个人电脑长期开着做服务器吧，但租用虚拟主机不仅价格不菲，而且服务和管理上也常常受制于人。（我现在就正为此而烦恼呢+_+）

　　就这个问题，我进一步在网上搜罗了一把相关的资料。原来WL-700gE采用的是Boradcom 4780MIPS 300Mhz CPU + 64M DRAM，由于有了160G的大容量硬盘助阵，Flash中的Boot loader也就无需做太多处理了，真正的操作系统被预置在硬盘中，而那就是我们所熟悉的**Linux**！Yeah, 这正是我们这些DIYer所希望的东西～ 想象一下Linux + Apache + MySQL组建而成的Web Server，绝对比那些廉价的虚拟主机服务强多了，更重要的是，它完全在自己的掌控之中。300MHz的MIPS CPU + 64M内存如果专职于Router+Server至少应付普通的个人或small business应用，我想应该是够用了吧？（期待尝鲜者的测试～）

　　呵，多么诱人的小家伙啊！不过在了解到它的零售价时，我着实汗了一把：**建议零售价为新台币8,890元 (约合人民币2,201元)**。罢了，还是等降价或者同类产品上市吧……