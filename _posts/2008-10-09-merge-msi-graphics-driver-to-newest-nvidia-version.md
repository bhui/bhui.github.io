---
id: 470
title: 移植微星显卡增强功能至最新nVidia驱动
date: 2008-10-09T00:28:15+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=470
permalink: /2008/10/09/merge-msi-graphics-driver-to-newest-nvidia-version/
dsq_thread_id:
  - "250427866"
  - "250427866"
categories:
  - Computer
tags:
  - mod
  - MSI
  - nVidia
---
微星显卡在nVidia显卡驱动的基础上提供了一些专有的增强功能（如D.O.T.和Vivid），但官方发布的版本是基于较老版本的nVidia显卡驱动制作的。如果希望使用nVidia的最新驱动，但又不愿失去微星的增强功能的话，就需要自己做一个移植工作了。

首先是准备工作。从微星网站下载的显卡驱动中提取出以下四个文件：

> MsiCpl.dll
  
> Startup.exe
  
> nv_disp.inf
  
> nvdisp.nvu

然后再从nVidia官方网站上下载最新版本的显卡驱动。因为下载的.exe安装文件其实是一个自解压包，可以使用WinRAR等工具展开；或者直接运行，在经过解压缩的步骤后推出安装程序。

下面开始实施移植。将上述从微星驱动中提取出的前两个文件MsiCpl.dll和Startup.exe直接复制到展开后的最新版nVidia驱动程序文件夹中。另外两个文件nv_disp.inf和nvdisp.nvu都需要手工与nVidia驱动程序的对应文件进行合并，将微星加入的部分同步到nVidia的驱动中。

以下是我针对nVidia的178.13 Vista 64bit International WHQL驱动版本修改好的上述后两个文件，仅供参考：

[17813\_geforce\_winvista\_64bit\_international_whql(msi)](http://blog.oasisfeng.com/wp-content/uploads/2008/10/17813_geforce_winvista_64bit_international_whqlmsi.zip)