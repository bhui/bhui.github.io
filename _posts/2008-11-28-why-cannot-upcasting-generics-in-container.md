---
id: 547
title: Java集合中的泛型为什么不能Upcasting？
date: 2008-11-28T19:40:08+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=547
permalink: /2008/11/28/why-cannot-upcasting-generics-in-container/
dsq_thread_id:
  - "250427987"
  - "250427987"
categories:
  - Development
tags:
  - cast
  - Container
  - Generics
  - Java
  - Upcast
---
典型的例子是：List<Object> objects = (List<Object>) new List<String>()

可能很多人（包括我在内）起初都会认为这是无法理解的。那么请看下面的代码：

objects.add(new Integer(7));

假设前述的类型转换成立，那么这个objects实例中不就可以加入新的Integer项了？这等于是破坏了List<String>的约束。由于这个反例的存在，所以上述类型转换是不被Java所允许的。