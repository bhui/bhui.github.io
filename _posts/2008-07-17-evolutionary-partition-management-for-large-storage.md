---
id: 322
title: 大容量个人存储时代的管理理念——分区管理篇
date: 2008-07-17T23:41:21+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=322
permalink: /2008/07/17/evolutionary-partition-management-for-large-storage/
dsq_thread_id:
  - "250427811"
  - "250427811"
categories:
  - Computer
tags:
  - disk
  - NTFS
  - partition
  - 分区
  - 盘符
  - 硬盘
---
当个人电脑的存储容量即将跨入TB纪元之时，你是否仍然还按照传统观念在管理着你的硬盘分区？将硬盘分作4-5个分区，分别规划为操作系统、应用软件、高清电影、网络下载、个人资料……

面对高达0.5-1TB容量的硬盘，不仅初期的分区容量规划变得难以取舍，一旦后期电脑应用趋势发生变化，分区的使用往往不得不偏离最初规划，而且还会造成文件存储的杂乱无章，甚至到头来连自己都找不到文件丢到哪里去了……

那么如何规划和使用你的硬盘分区才能最大程度的减少上述困扰呢？

<!--more-->

**（一）普通家庭用户**

对于普通家庭用户，这里推荐一种简单易行的方式：“小粒度片状分区” + “免盘符挂载”。举例而言，现在躺在我电脑中的一块320G硬盘，被我分成了13个分区，分别是：20G x 11 + 50G x 2。其中一个20G分区用于安装操作系统，另外10个20G分区则根据当前的应用需求进行合理分配。最后之所以特别划分了两个50G的分区，是专为Full HDRe影片准备的，因为这类影片的容量一般为12-20G，如果仍然使用20G大小的分区存储，则可能造成较大的剩余空间浪费。

如此一来，你可能会问，这么多分区，使用起来岂不是很麻烦，光是那一大堆盘符就看得人眼花缭乱了。没错，所以接下来将会提到另一个技巧——“免盘符挂载”，使用过Linux的朋友一定对其分区的“mount”管理方式非常喜欢，其实Windows也提供了相似的使用方式，前提是你需要NTFS文件系统格式的分区（在眼下这个年代，实在没有充分的理由再使用旧的FAT32分区格式了）。

[![Windows下进行免盘符挂载的操作界面](https://blog.oasisfeng.com/wp-content/uploads/2008/07/mount.jpg "免盘符挂载")](http://blog.oasisfeng.com/wp-content/uploads/2008/07/mount.jpg)

在“管理工具 &#8211; 计算机管理”中选择“磁盘管理”，然后在分区上点击右键，选择“更改驱动器号和路径”。在这里，你可以删除目前为其分配的任何盘符，然后点击“添加”并选择“装入以下空白NTFS文件夹中”，你需要浏览并选择一个NTFS分区上的空文件夹（记得先创建好这个空文件夹）作为其“挂载点”，也就是将要把这个分区映射到的虚拟位置。

最终，我将上面提到的11个分区用三个盘符组织起来：

<pre>C - Windows (20G)
E - Applications (20G)
    + Program Files (普通文件夹，用于安装一般的非绿色软件)
    + Programs (普通文件夹，用于存放我的绿色免费软件)
    + ... (其它普通文件夹)
    + Music (20G，挂载的另一个分区)
    + Video (20G，挂载的另一个分区)
    + Movie (20G，挂载的另一个分区)
    + Movie2 (20G，挂载的另一个分区)
    + Movie3 (20G，挂载的另一个分区)
    + ... (其它挂载的分区)
    + HD (50G，挂载的另一个分区)
    + HD2 (50G，挂载的另一个分区)
    + Download (10G, 挂载的另一个硬盘的分区，P2P下载的中转区)
P - Personal (20G，存储个人文件，为防止意外破坏，使用单独的盘符)</pre>

怎么样？按照这样组织文件还算简洁清爽吧？事实上，“小粒度片状分区”真正的价值是体现在其灵活的可调整性。比如后来，由于安装虚拟机调试程序的需要，我抽调了一个原先用于存储电影的20G分区划给虚拟机使用，这样既不破坏分区按用途命名和管理的原则，又充分而合理的利用了磁盘空间。

最后，作为一个附加的“收获”，磁盘碎片整理将不再让人望而生畏，因为至少我不必为电影、音乐、P2P下载暂存区等几类分区作碎片整理了。单个小分区的碎片整理将变得更加高效而易于计划。（友情提醒：你可能需要在“计算机管理”中选择没有分配盘符的分区启动碎片整理）

**（二）高级玩家**

（待续&#8230;）