---
id: 256
title: C语言小技巧：编译期ASSERT
date: 2007-06-25T21:47:54+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/06/25/compile-time-assert/
permalink: /2007/06/25/compile-time-assert/
dsq_thread_id:
  - "251137809"
  - "251137809"
categories:
  - Development
tags:
  - ASSERT
  - C
  - compile
  - sizeof
---
众所周知，ASSERT一般用于检查运行期的必备条件，它对编译过程没有任何影响，也不能在编译时阻止潜藏的错误。

常见的编译期ASSERT手段是使用 #if&#8230;#error&#8230;#endif 的结构，但由于#if之中的表达式是在预处理过程中计算，所以无法用到一些编译期才能确定的量，比如sizeof(&#8230;)。

无意中在Symbian的SDK头文件中发现一个有意思的宏，实现了真正的编译期的ASSERT：（简化整理后）

`#define COMPILE_TIME_ASSERT(expr)   typedef char assert_type[expr ? 1 : -1]`

它完全可以用于包含sizeof()等静态运算符的检查条件，同时，不会生成任何额外的二进制代码，也不依赖于特定的编译器，使用起来非常简单。但需要注意的是，参数expr只能是静态可计算的表达式，当然如果你不慎使用了非常量的表达式，编译器会阻止程序的编译，同样也起到了确保expr为常量的效果。