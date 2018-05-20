---
id: 900
title: 解决Cisco AnyConnect VPN客户端的DNS优先级问题
date: 2010-05-25T00:35:59+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=900
permalink: /2010/05/25/solve-the-dns-priority-issue-in-cisco-anyconnect-vpn-client/
dsq_thread_id:
  - "250427137"
  - "250427137"
categories:
  - Misc
tags:
  - AnyConnect
  - BAT
  - Cisco
  - DNS
  - VPN
---
Cisco AnyConnect VPN的客户端是一个工作于并行隧道（Split Tunnel）模式下的VPN软件，它可以方便的同时使用内外网两不误。它通过连接VPN后动态激活平时禁用的VPN虚拟网络适配器，并根据远端网关的配置应用相应的DNS和路由配置，实现了与默认网络环境无缝并行。但正是在其上述设计中的一个理想假设，为“中国特色”的互联网环境下使用它埋下了一个隐藏很深的问题。

如果你所连接的VPN网络本身是与Internet连通的，而且DNS也可解析外网的网址，由于AnyConnect会将VPN网络适配器的优先级提升到最高，因此远端的DNS配置会取代本地网络（例如家里的宽带网络）。如果你的本地网络和远程网络是同一接入线路，倒还感觉不到这之中的差别。但如果其中一个是电信线路，另一个是联通（网通）线路，你就会遇到一个很悲惨的状况：本地网络访问国内主要网站的速度会显著降低，因为DNS对大型网站CDN的解析结果是和你现有路由完全不同的线路，想象一下在你的联通（网通）宽带下访问电信线路的网站，那种感觉……

<!--more-->为了解决这个问题，我先后尝试了在注册表里静态调整适配器优先级、修改VPN适配器DNS配置等多种办法，但AnyConnect在每次连接时强制重置适配器配置和优先级的极端手段让我的大部分努力都付之东流。要不是公司网络只支持它家的VPN客户端，我真不想再看到这样一个流氓软件……

不得己，只好祭出最后的杀手锏，用批处理写了一个动态监视和修正DNS配置的脚本，放到任务计划中去自动执行。（眼看我的任务计划中已经塞了越来越多这类fix脚本，也只能留下一声叹息了……）废话不多说，直接上脚本：

anyconnect\_vpn\_dns_fix.bat

<pre>@echo off
set dns=127.0.0.1
:loop
netsh interface ip show dnsservers name="Cisco AnyConnect VPN Client Connection" | find "Cisco" &gt; nul
if errorlevel 1 goto sleep

netsh interface ip show dnsservers name="Cisco AnyConnect VPN Client Connection" | find "%dns%" &gt; nul
if errorlevel 1 goto fix

goto sleep

:fix
echo New Cisco AnyConnect VPN connection detected, apply the DNS fix...
netsh interface ip add dnsservers name="Cisco AnyConnect VPN Client Connection" address=%dns% index=1 validate=yes
goto sleep

:sleep
rem Sleep 10 seconds
ping -n 10 127.0.0.1 &gt; nul
goto loop</pre>

在将这个脚本丢进任务计划之前，还有几点需要补充说明：

  * 请将第二行的“127.0.0.1”改为你实际的宽带DNS服务器地址，比如路由器地址。
  * 这个脚本需要提升的UAC权限，因此务必在计划任务中设置“使用最高权限运行”
  * 为了消除丑陋的命令提示符窗口，建议使用[hstart.exe](http://www.ntwind.com/software/utilities/hstart.html)来启动它，用“/wait /noconsole”参数

用了这个脚本后，你可能会面临一个新的问题——VPN所连网域的内部域名无法正常解析了，而是跳到ISP的“网址智能纠错”页面中去了。这其实并不是上述脚本本身的问题，因为主DNS（即宽带DNS）无法解析的域名，本应传递给次DNS（VPN DNS），但却不幸遭遇了又一个典型“中国特色”互联网的变态产物——DNS劫持。对于这个问题的解决之道，请关注我的下一篇Blog：《中国特色互联网的生存法则——DNS免疫篇》