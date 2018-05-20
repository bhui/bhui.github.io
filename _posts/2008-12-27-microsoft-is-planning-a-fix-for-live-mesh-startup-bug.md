---
id: 568
title: 微软计划在一月份修复Live Mesh的启动bug
date: 2008-12-27T12:08:54+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=568
permalink: /2008/12/27/microsoft-is-planning-a-fix-for-live-mesh-startup-bug/
dsq_thread_id:
  - "268146100"
  - "268146100"
categories:
  - Internet
  - Software
tags:
  - Live
  - Live Mesh
  - Microsoft
---
如果你也尝试过使用微软的Live Mesh服务，并且“有幸”碰到了经典的启动问题：在你的某台电脑上无法正常启动Live Mesh，一直停在Live Mesh is currently starting，不出现登录提示。可以通过查看日志（%USERPROFILE%Local SettingsApplication DataMicrosoftLive MeshGacBaseMoe-*.log）中的“Get device certificate failed with IDCRL error 0x8004804E”确认这个问题。

那么有一个好消息是，微软看来已经准备好解决这个问题了。但由于问题似乎是出在Live Passport那边，因此修复工作最早也要等到下个月（2009.1）。

> FROM: Live Mesh Tech Preview Support <lmprev@microsoft.com>
  
> DATE: Sat, Dec 27, 2008 at 4:06 AM
  
> SUBJECT: 24614: DC11 &#8211; passport backend internal error &#8211; may prevent install
> 
> We are anticipating a Passport fix for this issue in the January time frame. We will follow up with you once the fix is released to make sure it worked for you. We apologize that we will not be able to take action on this issue sooner.
> 
> Thank you for this report!
> 
> Tim