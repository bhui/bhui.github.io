---
id: 358
title: C语言小技巧：带扫尾工作的宏
date: 2008-07-27T00:27:20+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=358
permalink: /2008/07/27/c-macro-with-tail-work/
dsq_thread_id:
  - "269017169"
  - "269017169"
categories:
  - Development
tags:
  - C
  - macro
  - 优化
  - 宏
---
前两天为了在C下编写一个类似Erlang式消息传递的框架，需要定义一个receive宏，使得coroutine处理函数的编写可以类似这样：

<pre>int foo()
{
    ...
    <strong>receive(msg)</strong>
    {
        // Deal with the message
    }
    ...
    <strong>receive(msg)</strong>
    {
        // Deal with another message
    }
    ...
}</pre>

因为foo()函数以coroutine方式执行，所以消息的及时释放就显得尤为重要了，receive()之后紧接的代码块就是这个消息的生存周期，完成之后需要立即对消息进行释放。这就对receive宏的编写提出了一个特别的要求：包含扫尾工作。

<!--more-->最后定义出来的宏是这样的：

<pre><strong>#define receive(msg) if (0); for (msg = co_recvmsg(); msg; co_freemsg(msg), msg = NULL)</strong></pre>

co\_recvmsg()是一个阻塞式的消息接收函数，co\_freemsg()就是那个负责释放消息的接口。开头的“if 0”则是为了避免当在同一层次中两次调用receive时使用相同的参数名可能导致的VC下编译错误（GCC没有这个问题）。

如果开启了优化选项，编译器将消除上述宏展开后的循环体，最终优化后的代码实际等效于：

<pre>// Source: receive(msg) { ... }
{
    msg = co_recvmsg();
    if (msg)
    {
        ...
    }
    co_freemsg(msg);
    msg = NULL;
}</pre>