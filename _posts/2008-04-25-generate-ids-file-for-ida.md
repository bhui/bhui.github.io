---
id: 308
title: 手动为IDA生成所需的导入符号映射表
date: 2008-04-25T01:45:22+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=308
permalink: /2008/04/25/generate-ids-file-for-ida/
dsq_thread_id:
  - "254437658"
  - "254437658"
categories:
  - Development
  - Symbian
tags:
  - dumpbin
  - IDA
  - ids
  - idt
  - sed
  - Symbian
---
IDA Pro 5.2自带了Symbian的导入符号映射表，但Emulator Build部分只含有Symbian 9系列的.ids文件。没有较早版本适用的，因为懒得去找旧版本IDA，所以自己写了下面这个批处理，可以快速的从.lib生成.ids，即IDA所需的导入符号映射表。

以.lib文件做参数时生成对应的.ids；不带参数则处理当前文件夹下全部的.lib文件。

<pre>@echo off
if %1. == . goto all
echo Process %1 ...
dumpbin /exports %1 | sed --text "/         [ ]*[0-9]*    /!d;s/^[ \t]*//;s/)$//;s/    / Name=/;s/ (/ Comment=/" > %1.idt
zipids %1.idt
goto end
:all
for %%f in (*.lib) do call %0 %%f
:end</pre>

注1：调用到的三个工具，dumpbin是VC6中包含的，sed可以用[UnxUtils](http://unxutils.sourceforge.net)中得到，zipids是IDA官方提供的附加工具包。
  
注2：只适用于Emulator Build，Target Build暂时还没有需求，因为IDA已经为Symbian提供了大部分.ids文件。