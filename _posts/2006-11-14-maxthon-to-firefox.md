---
id: 161
title: 从Maxthon到Firefox的尝试
date: 2006-11-14T00:08:38+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/11/14/maxthon-to-firefox/
permalink: /2006/11/14/maxthon-to-firefox/
dsq_thread_id:
  - "250426624"
  - "250426624"
categories:
  - Internet
  - Software
---
　　自从[上次介绍了Maxthon2 beta版](http://blog.oasisfeng.com/2006/11/07/maxthon2-beta1/)后，一位好友就开始极力游说我抛弃IE内核，转投Firefox，并为我列举了一大堆的好处。盛情难却，我只好答应试用一下Firefox2。

　　其实，我并非没有接触过Firefox，相反，从1.0beta版开始，我就已经让Firefox在我的硬盘中落户了。但真正阻碍我将Firefox作为主用浏览器的关键因素还在于当时的Web并没有完全接受Firefox，所以有相当一部分网站无法在Firefox中正常显示。另外，初期的Firefox在易用性方面相对Maxthon来说还略微欠缺（那时候还没有广泛的插件支持）。

　　转眼间，Firefox已经发展到2.0，而且在浏览器领域已经占据了重要的一席，这也迫使越来越多的网站开始重视XHTML标准的遵从，而非一味的为IE优化。不过，长期使用Maxthon之后，在操作习惯上形成了一定的依赖性，要转投Firefox可能还真有点不适应。直到试用之后，我才发现，其实原来完全不需要抛弃固有的操作习惯，借助Firefox强大的插件系统，我们甚至可以打造一个Firefox版的Maxthon呢。下面且听我一一道来：

<!--more-->（1）首要解决的仍然是兼容性问题，如何让Firefox完全兼容IE优化的网站呢？

[IE tab](https://addons.mozilla.org/firefox/1419/)这款插件为我们提供了一个简单但非常有效的解决方案。通过在Firefox内嵌入一个IE内核，使得你不必单独开启IE就能兼容并包了。:)

（2）其次，Maxthon中我用的最多也是几乎离不开的一个特性：超级拖拽——轻拖一个链接，顺手一甩就在新的tab中打开了。（不知道是不是Maxthon首创的？）好在已经有一个名为[Super DragAndGo](https://addons.mozilla.org/firefox/137/)的插件在Firefox中实现了一摸一样的功能，大大的方便了我这种甩上瘾了的人。

（3）刚开始试用Firefox时是否觉得它的tab功能未免显得太单薄了一点？没关系，有了[Tab mix plus](https://addons.mozilla.org/firefox/1122/)，Firefox中的tab也能随心所欲的操控，甚至比Maxthon还更为强大、易用。

（4）上次我在引荐Maxthon2时，提到了一个非常人性化的功能——高级代理策略（为某些网站自动绑定代理）。如今才发现，原来这个功能早已在[FoxyProxy](https://addons.mozilla.org/firefox/2464/)插件中实现了，而且比Maxthon2更成熟和稳定。（我在Maxthon2中匹配Google Cache总是不行……）

（5）Maxthon的广告过滤功能说不上特别强大，但习惯之后基本算是比较顺手，而且Maxthon2中更是大大增强了广告过滤，支持代码级别的过滤和过滤规则包。但令我没想到的是，在[Adblock Plus](https://addons.mozilla.org/firefox/1865/)插件面前，Maxthon2这些看似强大的功能也最多只能算是打个平手。而且Adblock Plus的优势在于已经较为成熟的过滤规则社区。普通用户只需要简单的订阅一下相应社区的规则，即可坐享其成了。（唉，想当初我还自己满大街的添加广告过滤规则…… >_<） 　　除了上面提到的这几个优秀的插件外，还有一些值得推荐的插件，我就不作一一介绍了，有兴趣的朋友可以具体了解它们的用途： [All-in-One Sidebar](https://addons.mozilla.org/firefox/1027/)
  
[Download Statusbar](https://addons.mozilla.org/firefox/26/)
  
[GreaseMonkey](https://addons.mozilla.org/firefox/748/)
  
[FasterFox](https://addons.mozilla.org/firefox/1269/)
  
[Web Developer](https://addons.mozilla.org/firefox/60/)

　　BTW，刚从Maxthon切换过来时，发现Firefox似乎对默认浏览器的注册存在一个bug，从外部打开的链接竟然仍是关联到Maxthon的。后来分析注册表才发现，Maxthon修改了关联的默认行为，原本的“Open”被改为新增的“Maxthon”，Firefox对此未作任何检查……