---
id: 884
title: Google Wave终于支持非Wave用户匿名浏览
date: 2010-04-17T13:56:03+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=884
permalink: /2010/04/17/google-wave-finally-support-for-anonymous/
dsq_thread_id:
  - "250428378"
  - "250428378"
categories:
  - Development
tags:
  - API
  - Google
  - openid
  - Wave
---
下面这个嵌入式的Wave就是Google Wave团队的官方公告Wave，现在你不用登录Wave就能看到它了。不过匿名用户还只能浏览，参与互动仍然需要登录。但这样已经让Google Wave的可用性大大增强了，可以在更多Web领域发挥它应有的价值。

结合Google Wave API的[Proxying-for](http://code.google.com/apis/wave/extensions/robots/operations.html#Proxying)，我们也可以自己实现匿名式交互，或者与其它身份系统集成（比如OpenID）。有时间的话，我会尝试做一个OpenID Proxy的Sample。