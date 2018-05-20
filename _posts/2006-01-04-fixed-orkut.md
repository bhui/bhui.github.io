---
id: 77
title: 搞定Orkut了，just so simple
date: 2006-01-04T01:48:28+00:00
author: oasisfeng
layout: post
guid: 'http://www.oasisfeng.com/blog/2006/01/04/%e6%90%9e%e5%ae%9aorkut%e4%ba%86%ef%bc%8cjust-so-simple/'
permalink: /2006/01/04/fixed-orkut/
categories:
  - Internet
---
初步推测是由于Orkut的个人设定FORM中 First name 和 Last name 都在loot focus，如果在这两个field间切换就会形成死锁（从一个侧面反映IE的弱智……）。

基于以上分析，我采取了修改 First name 后不跳到其它域，也不点“Update”按钮（这个时候点也一样无效），而用最直接的方式——“回车键”，Bingo，修改成功！Last name同理～

最后，例行鄙视一下合作完成这个bug的两个傻瓜 —— Google & Microsoft ^_^