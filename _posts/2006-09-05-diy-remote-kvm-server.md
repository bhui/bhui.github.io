---
id: 93
title: DIY简易的Remote KVM Server
date: 2006-09-05T22:46:38+00:00
author: oasisfeng
layout: post
guid: 'http://blog.oasisfeng.com/2006/09/05/diy%e7%ae%80%e6%98%93%e7%9a%84remote-kvm-server/'
permalink: /2006/09/05/diy-remote-kvm-server/
dsq_thread_id:
  - "250426208"
  - "250426208"
categories:
  - Computer
tags:
  - Computer
---
Keywords: Remote KVM、IPMI、Intel

　　因为实验室和办公室实在是相隔十万八千里，所以我经常会打一些懒主意，尽量减少往返于两地的次数。

　　今天无意中在Intel Server Board的BIOS中发现了Remote KVM这个玩意儿，才发现原来远程管理还可以这样玩。:)

<!--more-->　　以往为了远程操作服务器单板，都是通过SSH或者X11进行远程登录，但最近在进行Linux内核方面的实验，一旦启动失败了，往往就只得“奔赴现场”进行处理了…… 毕竟基于软件的远程登录协议一般都不能脱离操作系统而存在。但Remote KVM就不同了，它是基于硬件的远程管理，完全由BIOS实现。其实它的原理是很简单的：通过BIOS将Keybord、Video、Mouse三大核心输入输出设备进行重定向，以便远程进行底层级别的管理任务，比如修改BIOS、安装操作系统等。

　　在网上查了一下相关的资料，原来Intel的实现是将KVM重定向到串口，然后通过一块专用的Remote Management Module单板将串口的数据进行汇聚、编解码并通过TCP/IP提供给远程的终端访问。说到底，Intel还是很有商业头脑的，毕竟这么一块RMM单板就可以卖$XXX了……

　　我当然不能为了自己的懒惰而向Boss申购一块RMM，那么只好自己DIY一个“土”一点的Remote KVM Server了。实验发现，在文本显示模式下，KVM重定向到串口的数据流基本是符合VT100。于是一个初步的方案就这样形成了：用一台Win2000 Server的主机将串口连接到Intel Server Board上，然后开启终端服务。于是，只要在办公室的电脑上用RDP客户端连接上Win2000服务器，然后在远程会话中运行“超级终端”，就可以初步实现Remote KVM。

　　试验了一下，基本的功能算是达到了，但显示模式仅仅支持最基本的滚屏式文本模式，如果想远程进入BIOS设置界面的话，就什么内容也看不到。实际上在单板上是进入BIOS设置，但全屏式文字模式在目前这个简陋的方案里还支持不了，所以也谈不上操作了。另外，虽然在进入图形界面的Grub后，也看不到任何内容，但却可以完全“盲目”的用方向键选择需要启动的项，这样就再也不怕试验用的Linux内核挂掉了。配合IPMI协议中的远程复位指令，终于可以完全坐镇办公室，运筹帏幄与千里之外了。^_^Y

　　尾注：以后再仔细分析一下Intel的KVM传输协议，或许通过调整配置可以实现全屏式文本模式，那样整个方案就具备很高的可用性了。不过Mouse恐怕是不可能在这个方案里实现了，那么少了一环的话，或许称作Remote KV才恰当吧？= =!