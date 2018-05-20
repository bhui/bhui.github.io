---
id: 310
title: 在Windows Vista/2008下搭建Symbian开发环境
date: 2008-05-10T09:23:39+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=310
permalink: '/2008/05/10/%e5%9c%a8windows-vista2008%e4%b8%8b%e6%90%ad%e5%bb%basymbian%e5%bc%80%e5%8f%91%e7%8e%af%e5%a2%83/'
dsq_thread_id:
  - "250427713"
  - "250427713"
categories:
  - Development
  - Symbian
tags:
  - EPOC
  - GCC
  - Symbian
  - Vista
  - Windows 2008
  - 虚拟机
---
升级到Windows Server 2008后，面临最大的一个挑战便是Symbian开发环境的迁移。让Carbide + S60第三版SDK 工作在Vista下的讨论已经比较多了，实现起来也并不复杂，所以本文主要关注Symbian 6.1等低版本OS的迁移问题，并以Nokia S60 SDK 1.2在Windows 2008 (x64)为蓝本进行说明，方法同样适用于Symbian 7.0s/8.1和Windows Vista (x86/x64)系统。

兼容性问题主要集中在GCC和模拟器上，后者相对比较容易，只需赋予管理员运行权限即可。GCC则是一个真正的麻烦事儿，由于它是Symbian为其工具链所改造的一个GCC 2.9的私有版本，不同于主版本分支，目前也没有继续的维护者[<sup><strong>[*]</strong></sup>](#remark1)。Vista之后版本的Windows由于DEP和安全性保护的增强，使得GCC在编译中会出现“Exception: STATUS\_ACCESS\_VIOLATION”错误，即使定向关闭DEP或者完全关闭DEP也无济于事。为GCC工具所有的执行文件赋予管理员权限同样不管用，错误表现可能会有差异，但结果都一样。

<!--more-->折腾了两天后，仍然无法解决GCC在2008下的运行问题，只好迂回突进——在虚拟机中运行GCC。好在一般的模拟器版本编译和调试还不必如此麻烦，只需在编译手机版本时才使用虚拟机。微软提供免费的Virtual PC 2007可以很好的胜任这一使命，不过其“Folder Share”机制的性能真的是出乎意料的差，还不如通过映射网络驱动器速度快。在虚拟机中安装XP或者2003都没问题，移植编译环境比较简单，只需注意以点：

（1）手机编译工具链依赖VC的nmake，最简单的办法是直接提取出“nmake.exe”和“MSVCR71.DLL”两个文件，放在PATH环境变量包含的路径中即可。
  
（2）不用在虚拟机中再安装SDK，直接将你住操作系统中SDK所在的驱动器通过网络映射到虚拟机中，并配置好PATH就行了。
  
（3）Perl也可以如法炮制，PATH中记得加入“x:perlbin”。

Virtual PC比较实用的一个功能就是直接挂起虚拟机，这样每次编译完后挂起，下次激活虚拟机马上就可以启动编译，而不必重新启动其中的Windows。大大降低了因为引入虚拟机而带来的效率损失。

<a name="remark1"></a> [*]注：Symbian GCC曾经有一个民间组织在维护其[优化后的版本](http://www.inf.u-szeged.hu/symbian-gcc/)，他们最后一次成功的移植是GCC 3.0。改天有时间来验证一下这个版本是否可以在2008下不借助虚拟机直接运行。