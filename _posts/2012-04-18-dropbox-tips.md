---
id: 1062
title: Dropbox使用技巧拾零
date: 2012-04-18T00:02:53+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=1062
permalink: /2012/04/18/dropbox-tips/
dsq_thread_id:
  - "653264579"
  - "653264579"
categories:
  - Internet
  - Software
tags:
  - Dropbox
  - Git
---
Dropbox可以算是文件云同步领域的鼻祖了，即使不是最早出现的，也是第一个推动云同步向普通互联网用户普及的。Dropbox的成功并非偶然，其强大而且独一无二的功能和技术是支撑其用户忠诚度的基石。作为一个Dropbox的早期用户，使用至今，有些小经验小技巧，在这里与大家分享一下，希望能帮助大家把Dropbox的作用发挥到最大。

### 值得信赖的差量同步

『差量同步』是Dropbox相比其它同类云同步工具的核心技术优势。其效果可以简单理解为，文件的变更只需同步变化的部分，为用户节省流量和时间。差量同步所带来的好处其实还不仅仅是文件的变化同步更快，你还可以随心所欲的将文件或整个文件夹从Dropbox下的一个位置移至另一个位置、更名，甚至拿掉一段时间之后再放回来，它们都不必重新被上传到服务器。而其它云同步工具就未必能这么省心了。

Dropbox的其它一些特性，也是建立在这个机制之上的。就拿『文件历史』功能来说，别担心Dropbox会消耗数倍的空间来保存文件的历史版本，其实它只是保存了多个版本的差异，这样消耗的空间通常是非常少的。

得益于强大的差量同步，你甚至可以在Dropbox之上构建其它存储技术，并保持高效率的同步。比如在Dropbox中使用TrueCrypt，由于后者对加密数据的变更作用到卷文件上体现为局部的变化，所以可被Dropbox高效的同步，而完全不必担心一点变化而导致整个庞大的卷文件需要重新上传，这是其它一些云同步工具所无法比拟的。不过，在这类场景下需要非常小心『变更冲突』可能带来的不良后果（产生两份不和谐的副本），尽可能不要同时在多处对数据进行修改。

### <!--more-->善用选择性同步（Selective Sync）

选择性同步是Dropbox早期呼声最高的期望特性，没有之一。不过这个特性足足让大家等了一年多，才最终被开发团队满足。背后故事的曲折就不赘述了，好在现在的这套实现方式应该还算是比较让人满意的。选择性同步的使用场景非常广泛，下面简单列举几个，大家也可以根据自己的需要自由发挥：

  * 避免在非主用电脑上同步包含备用资料、音乐、视频的大文件夹。
  * 避免在笔记本电脑上同步敏感私人数据。
  * 避免同步.svn文件夹，最好配合支持归一svn文件夹的新版SVN客户端。
  * 避免同步系统或应用程序频繁自动生成的文件，比如某些临时文件夹、Java开发工程的target/bin/gen文件夹。
  * 避免同步与本地电脑环境（如绝对路径）相关的数据，比如引用了绝对路径的Java工程中的.project文件、某些应用程序的配置文件。
  * ……

### 更简单实用的分享功能

Dropbox发展到今天，共享功能几经优化，已渐趋完善。现在你不仅可以在网络上开放的分享Dropbox中的某个文件或文件夹，而且还能有选择的在几个朋友或同事之间私密的共享一个文件夹，并保持它在多人之间的实时同步。多人共享功能需要其它人也有Dropbox账号，但不必一定使用客户端。现在我就经常利用多人共享功能和朋友共享一些技术书籍电子版、合作收集一些素材、交换最近出行的照片，甚至替代SCM工具直接作为简单开发工程的多人同步方式。因为简单，所以方便！

### Git over Dropbox

这里特地把Git拿出来单独讲，是因为我在这个使用场景下摸索了一段时间才找到最佳的使用方式，与大家交流一下。通过Git分布式的管理代码是现在主流的SCM解决方案，但在多人之间协作时，往往还是绕不开一个中心服务器。Git Hub或者Bit Bucket是不错的选择，但繁琐的配置和网络的等待让这个方案变得有点难受。其实Git over Dropbox就是一个简单易行的入门级解决方案，不仅适合小团队，还可以用作个人的代码管理。

如果是个人使用，我倾向于直接将整个工程，连同.git子文件夹一并放在Dropbox上。表面上看起来是有些冗余，不过好处是，不仅git中的数据在云端自动备份，尚未commit的代码也保证了同步，方便有时即使有尚未写完的代码，也不必为了保持同步而commit进去污染仓库，回到家里还可以继续调试完善。

倘若需要多人协作，则建议将工程与git分离，只在Dropbox上创建bare repo (git init &#8211;bare)，大家将各自Dropbox中同步的bare repo作为remote进行push/pull或clone。不过，这种方案其实是以让渡一致性换取异步同步的便捷性，所以不适合大量开发人员的频繁git操作，那样容易引入让人头疼的同步冲突。

### 正确使用『内网优先同步』

这是Dropbox从很早版本就支持的一个特性，但却鲜有人知晓和使用。这个按照简单原则所设计的产品功能，在现实情况下，往往并不如其所设想的那么奏效。『内网优先同步』要求同步的多点在同一个子网（广播域）下，所以如果电脑之间的连接跨越了路由器，则在物理上阻断了这个特性的正常工作。

另外，防火墙也必须允许Dropbox的端口侦听。需要注意的一点是，当Dropbox检测到防火墙阻断其端口侦听时，会自动关闭这个功能，所以在正确设置了防火墙之后，还应检查Dropbox的配置中是否激活了『Lan sync』。

值得一提的是，『内网优先同步』除了可在同一账号的多台电脑间快速同步文件外，还支持多人的共享文件夹同步。所以小团队在局域网内使用这个功能是一个非常简单而高效的文件共享解决方案。

### 奖励空间的最大化

Dropbox依仗其技术优势和行业地位，在空间的给予上明显有些吝啬了。普通注册用户只有2G空间，通过<a title="Affiliate link" href="http://db.tt/weEV0ID" target="_blank">邀请注册</a>勉强能得到2.5G的初始容量，不过只是杯水车薪了。其实，Dropbox提供的一些空间奖励计划能帮你快速增加不小的空间，而且操作难度并不大，比如邀请一个好友可以得到500G空间（本来还想写如何认证学生账号获得双倍奖励，可惜最近也给扯平了）。

其实，有一个隐藏颇深的<a href="https://www.dropbox.com/free" target="_blank">奖励任务入口</a>，可能大部分Dropbox用户都未必发现并完成了其中的任务。完成诸如链接Twitter/Facebook账号、follow @Dropbox、发表感言等小任务，就可以得到640M的额外空间，虽然不算多，倒也不拿白不拿。

* * *

如果你还不是Dropbox的用户，觉得我写的这篇内容还算有用，让你有了一试Dropbox的冲动，那么不妨<a title="Affiliate link" href="http://db.tt/weEV0ID" target="_blank">用我的推荐链接注册</a>，咱俩各获得500M的奖励空间，何乐而不为呢？ (: