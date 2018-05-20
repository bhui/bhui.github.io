---
id: 466
title: nVidia显卡驱动与Hyper-V存在冲突
date: 2008-10-08T23:31:00+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=466
permalink: /2008/10/08/nvidia-display-driver-conflicts-with-hyper-v/
dsq_thread_id:
  - "257555007"
  - "257555007"
categories:
  - Computer
  - Software
tags:
  - Hyper-V
  - nVidia
  - Windows2008
---
在折腾了数天后，终于查出导致Windows 2008系统出现性能问题的罪魁祸首。话说前几日在新系统上安装Windows Server 2008后，在诸多场合下出现了显著的响应变慢，甚至长时间停滞的问题，例如最大化窗口需要3-5秒时间、初始化3D显示时约有5秒以上的延迟，打开视频文件则伴随长达半分钟左右的停滞……

最终，经过反复重装系统、安装/卸载软件的折磨，终于发现问题出在nVidia的显卡驱动程序与Hyper-V有冲突。只要卸载掉两者中任一，上述症状就全部消失了。在Hyper-V的技术论坛中找到了[类似的问题反馈](http://social.technet.microsoft.com/Forums/en-US/winserverhyperv/thread/4e1c53f5-0400-4ca9-8819-f942c10881c1)，而且有人证实ATI的显卡驱动没有问题，甚至有比我还有受虐倾向的强人，测试了过去18个月以来nVidia所发布的驱动程序，直到找到v100版本据说没有上述问题…… 发帖人在向微软提交bug后也得到了技术人员对此问题的确认，可惜目前暂无解决措施。

唉，本就冲着Hyper-V才安装Windows 2008，现在倒成了近在眼前美味的吃不到…… 亏得我放弃了多年的合作伙伴ATI而选择nVidia的显卡，结果竟遭遇如此折磨！