---
id: 541
title: 当心应用软件借安装程序绕过UAC
date: 2008-11-16T23:07:15+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=541
permalink: /2008/11/16/do-not-directly-start-application-as-suggested-in-its-installer/
dsq_thread_id:
  - "250427951"
  - "250427951"
categories:
  - Computer
tags:
  - Installer
  - Security
  - UAC
---
如果你仍像我一样谨慎的依托UAC保护自己的Windows系统，那么就不能不提防一种应用程序常见的绕过UAC保护的伎俩。

通常很多应用软件在安装结束前都会给出一个选项（默认选中），让你可以方便的在安装完成后直接启动之。这时千万不要让它这样做，因为应用软件自身作为安装程序的一个子进程启动，便会继承其父进程的全部既得权限。我们知道，安装程序作为一类特殊的程序，一般都会要求用户赋予其管理员权限以完成正常的安装动作。在它名正言顺的拿到尚方宝剑后，再将其暗度陈仓的传递给安装后的应用程序，这样一来就有机会背着用户越权执行一些危险动作了。

基于上述原因，大家切忌不要允许安装程序结束时直接启动安装后的软件，以防被无良软件所坑害。