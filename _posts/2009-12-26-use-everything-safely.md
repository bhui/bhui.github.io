---
id: 832
title: 安全的使用Everything
date: 2009-12-26T20:04:31+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=832
permalink: /2009/12/26/use-everything-safely/
dsq_thread_id:
  - "250428282"
  - "250428282"
categories:
  - Software
tags:
  - Everything
  - hstart
  - Total Commander
  - UAC
---
相信大部分用过<a href="http://www.voidtools.com/" target="_blank">Everything</a>的朋友们都再也离不开它了，我也一样。作为一个现今已不多见的“键盘流”，日常的大部分程序我基本都直接从Everything中启动，少了纷乱的快捷方式，桌面也清爽了不少。

Everything由于核心原理建立在NTFS的底层机制上，所以在Vista/Win7中不可避免的必须以提升的权限运行（UAC），不过这对与大多数PC玩家来说早已不算什么障碍。但你是否留意过，通过Everything启动的任何程序或打开的任何文件，也都继承了其拥有的提升权限，这对于重度依赖它的玩家来说，却是一个非常致命的隐患。当你从Everything中启动了Total Commander，又从Total Commander中启动其它应用，这整个程序链全都跑在不受约束的管理员权限下，对系统安全构成了严重的威胁。

那么，如何才能避免这种权限提升的传递呢？

<!--more-->好在Everything本身提供了非常全面的扩展机制，只要修改其everything.ini文件就可以修补这个安全漏洞了。打开ini文件，搜索“%1”便可以找到用于Everything启动其它程序的选项将其修改为：

<pre>explore_folder_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "%SystemRoot%explorer.exe" /n,/e,"%1")
explore_folder_path_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "%SystemRoot%explorer.exe" /n,/e,/select,"%1")
open_file_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "%1")
open_folder_path_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "%SystemRoot%explorer.exe" /n,/e,"$parent(%1)")
open_folder_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "%SystemRoot%explorer.exe" /n,/e,"%1")</pre>

如果你用的是Total Commander作为文件管理器，那么后两行需要改为：（别忘了把“X:TotalCmd”替换为Total Commander的实际路径）

<pre>open_folder_path_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "X:TotalCmdTotalCmd.EXE" /t /o /r="$parent(%1)")
open_folder_command=$exec("%SystemRoot%System32runas.exe" /trustlevel:0x20000 "X:TotalCmdTotalCmd.EXE" /t /o /r="%1")</pre>

经过上述修改后，你再从Everything中启动的程序或打开的文件，就只有正常的受限权限了。但由于Windows自带的“runas.exe”使用console方式运行，会在启动瞬间弹出一个一闪即逝的“黑窗口”。如果你不习惯的话，可以去下载一个<a href="http://www.ntwind.com/software/utilities/hstart.html" target="_blank">“Hidden Start”</a>，然后将上述ini文件中的内容替换为：

<pre>explore_folder_command=$exec("X:hstart.exe" /nonelevated ""%SystemRoot%explorer.exe" /n,/e,"%1"")
explore_folder_path_command=$exec("X:hstart.exe" /nonelevated ""%SystemRoot%explorer.exe" /n,/e,/select,"%1"")
open_file_command=$exec("X:hstart.exe" /d="$parent(%1)" /nonelevated "%1")
open_folder_path_command=$exec("X:hstart.exe" /nonelevated ""%SystemRoot%explorer.exe" /n,/e,"$parent(%1)"")
open_folder_command=$exec("X:hstart.exe" /nonelevated ""%SystemRoot%explorer.exe" /n,/e,"%1"")</pre>

或对于Total Commander：（别忘了把“X:TotalCmd”替换为Total Commander的实际路径，“X:HStart”替换为Hidden Start的实际路径）

<pre>open_folder_path_command=$exec("X:HStartHStart.exe" /nonelevated ""X:TotalCmdTotalCmd.EXE" /t /o /r="$parent(%1)"")
open_folder_command=$exec("X:HStartHStart.exe" /nonelevated ""X:TotalCmdTotalCmd.EXE" /t /o /r="%1"")</pre><hr size=2> 

**2010.6.25 更新: open\_file\_command 配置中给 hstart.exe 增加 /d 参数指定程序的启动路径为程序所在位置。**</p>