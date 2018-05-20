---
id: 321
title: 打点一个整洁的任务栏——三款免费任务栏整理工具横向评测
date: 2008-07-14T02:09:20+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=321
permalink: /2008/07/14/tidy-up-your-taskbar/
dsq_thread_id:
  - "250427828"
  - "250427828"
categories:
  - Computer
  - Software
tags:
  - Freeware
  - taskbar
  - tray
  - treak
  - Windows
---
　　如果电脑是你的主力生产工具，那么工作中通常难以避免打开一大堆窗口，尤其是碰到那些不支持Tab或MDI模式的应用程序。而且搞不好排列混乱的任务栏以及手忙脚乱的找窗口还会破坏你工作时的好心情，让你陷入无谓的抓狂之中。

　　从某种角度来说，自Windows95至今，正是微软对这个设计简陋的任务栏顽固之极的坚持，自然而然的催生了一系列任务栏优化工具。这次要拿出来分享的就是一类应对上述问题而生的“任务栏按钮整理工具”。经过一段时间的收集和试用，大致挑选出以下三款小工具（均为绿色免费软件）：

<!--more-->

[Taskbar++ v1.2](http://hp.vector.co.jp/authors/VA013430/program/taskbarpp/main.html)

　　这是一位日本朋友写的小程序，也是最早出现的此类工具（鼻祖？），功能简单朴素，但足够满足大部分人的需求（包括我）。可惜已经许久没有升级过了。

[Taskbar Shuffle v2.5](http://www.freewebs.com/nerdcave/taskbarshuffle.htm)

　　估计是受到楼上的启发，这位颇具才华的仁兄索性将“任务栏整理”这个主题的内涵与意境发挥到了极致，创造出了这个同类软件中最受欢迎的选择。舒适的半透明效果，细微的平滑动画处理让人有种爱不释手的感觉（要是还能进一步实现Aero Glass的磨砂效果，那就完美了~ \*_\*），而附加对托盘图标整理的支持更是锦上添花。
  
最后忍不住再赞一下这款软件，它整合了对Windows任务栏分组机制的精细调整选项，虽然这并不是Taskbar Shuffle提供的特性，但它以一种通俗易懂的方式呈现给了用户，比TweakUI等工具中类似的调整选项友好了很多。

[Taskix32 v1.5](http://taskix.robustit.com/)

　　最后出场的这位小兄弟，别看其貌不扬，甚至没有任何配置选项（除了“随Windows自动启动”），但却最终赢得了我的选择。原因很简单，它是三者中唯一支持x64版本Windows的。

为了公平对比上述三款软件，我选择了Windows XP的32位版本作为测试平台，并在一个实际的具有相当测试压力的PC环境中进行本次测试。（512M物理内存基本耗尽，页面文件使用量接近1G。怎么样，压力够大吧？- -!）

废话不多说，直接来看测试结果：（表格嵌入自Google Docs，如果在RSS阅读器中无法看到，请进入Blog页面观看）



总结：

　　我最早发现了Taskbar++，并且使用了相当长一段时间，虽然要按住ALT键移动任务栏按钮，但用久了也就习惯了，Taskbar Shuffle和Taskix都是在迁移到Windows Server 2008 (x64) 后无法继续使用Taskbar++而迫于无奈去网上搜寻到的，它们都是同类软件中的翘楚。总的来说，对于大部分使用32位Windows系统的普通用户，推荐使用Taskbar Shuffle，完善的功能和有亲和力的视觉效果，你又怎会因此而责难它稍多一点的内存占用呢。如果你的机器较老，或者是极端的资源敏感群体，亦或是一个简约主义者，那么Taskix一定能成为你的最爱！而Taskbar++就实在没有向大家推荐的理由了。（怀旧&#8230;？好吧，如果你不抵制日货的话。）
  
　　上述三款软件均与虚拟桌面类工具有冲突，比如微软WinXP PowerToy中的Virtual Desktop Manager。整理过的任务栏只要进行桌面切换，则任务栏按钮的排列又会还原到无序状态。原因是后者的桌面切换核心机制是依靠保存和恢复任务栏按钮实现的，而它显然没有感知到任务栏按钮已经被用户手工整理过，而仅仅是按照其内定的原则来恢复任务栏按钮的次序。

小技巧：

　　利用TweakUI等优化工具将任务栏分组的窗口数目下限设为一个较大的数字（比如100），就可以实现自动聚集同类按钮但不合并成组的效果。比如你打开了多个记事本窗口，它们会自动靠拢在一起，即使中间曾打开过其它窗口。在特定的场景下，对于提高工作效率有非常显著的效果。这个技巧其实可以不必依赖于任何第三方软件，导入下面的注册表文件即可：

<pre>Windows Registry Editor Version 5.00

[HKEY_CURRENT_USERSoftwareMicrosoftWindowsCurrentVersionExplorerAdvanced]
"TaskbarGroupSize"=dword:00000064</pre>