---
id: 301
title: 打造绿色版uTorrent
date: 2008-01-19T10:38:42+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2008/01/19/greenize-utorrent/
permalink: /2008/01/19/greenize-utorrent/
dsq_thread_id:
  - "250427698"
  - "250427698"
categories:
  - Software
tags:
  - BT
  - uTorrent
  - 绿色软件
---
uTorrent下载下来就只有一个执行文件，随便放在哪里都可以运行，很多人（包括我）可能会误以为它就是原生的绿色软件。而uTorrent最近的版本增加了“自安装”功能更是让人糊涂：当你升级到新版本时，第一次运行时会询问你是否安装，回答“是”的话它就会将自己复制一份到%ProgramFiles%utorrent下，然后继续以当前位置这一份运行；回答否则跟过去一样，直接从当前位置运行。

其实uTorrent默认情况下并不是按照绿色软件的方式运作的，因为它考虑了多用户的配置隔离问题：每个用户都有一份属于自己的参数配置和下载状态，彼此互不影响。那么如何让所有用户共用相同的配置，也即将uTorrent打造为绿色版呢？官方FAQ给出了一个简单的方法：

> 将%AppData%uTorrent下面的所有文件移动到跟utorrent.exe相同的文件夹下即可。

这样一来uTorrent就变为纯粹的绿色软件了，这里说“纯粹”是因为uTorrent本身可以完全不修改注册表。（当然，关联种子文件除外）