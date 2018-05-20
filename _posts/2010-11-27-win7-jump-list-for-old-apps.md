---
id: 982
title: 让旧软件也用上Win7任务栏的Jump List
date: 2010-11-27T19:56:09+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=982
permalink: /2010/11/27/win7-jump-list-for-old-apps/
dsq_thread_id:
  - "250428447"
  - "250428447"
categories:
  - Software
tags:
  - Jump List
  - putty
  - taskbar
  - Windows 7
---
Windows 7 强大的 Jump List （跳转清单）特性大大提升了我们日常应用的便捷性，随着越来越多的应用程序对它的支持，Jump List 已经成为了大家 Windows 操作习惯中的重要部分。

可惜一些旧时的应用软件，或者软件开发者没有引入对 Jump List 的支持，就难以从中获益了。不过，Windows 7 本身还是给我们预留了一定的定制空间，只要稍加利用，也可以为这些旧软件整合 Jump List 的新体验。根据软件控制方式的不同，一般有两种整合方式：

<!--more-->

**（1）文件关联型的应用**

主要指文件查看、编辑、处理类的应用软件，其共同特点是都会关联特定的文件扩展名，他们整合 Jump List 相对比较简单。

首先，你需要将其锁定到任务栏：启动一次该应用软件，然后在其任务栏标签（图标）上点右键，选择 “将此程序锁定到任务栏”。
  
其次，需要确保他们正确的关联到了相应的文件扩展名。如果尚未关联，可以找一个该扩展名的文件，在右键菜单中选择 “打开方式” &#8211; “选择默认程序&#8230;”。
  
然后，通过双击打开上述扩展名的文件，这个文件就会出现在该应用软件的 Jump List 中（“最近” 分组下）。
  
如果想要将某个文件固定在 Jump List 中，除了可以在 “最近” 分组下点击文件名右侧的图钉图标，还可以将文件直接拖拽到这个应用的任务栏图标（标签）上。

**（2）支持命令行参数的应用**

如果某个应用不具备文件关联性，那么集成到 Jump List 中的过程则相对复杂一些，不过基本思路仍然是基于以上方式（1）的延伸。下面就以 Putty（一款支持命令行参数的SSH客户端） 为例，说明如何操作。

首先，我们需要为其杜撰一个特殊的文件扩展名作为与 Jump List 衔接的桥梁，比如 “.ssh”。建立一个名为 session-name.ssh（将 “session-name” 换成 Putty 中保存的 session 名称） 的空文件，然后双击该文件，通过 “从已安装程序列表中选择程序” 将其关联到 “Putty.exe”。这时你会看到一个 Putty 的错误信息，告诉你无法打开，请忽略它。那是因为 Putty 并不支持文件关联的方式。

然后，我们进入注册表编辑器，找到 “HKEY\_CLASSES\_ROOTssh\_auto\_filePutty.exe”，展开其下的 “shellopencommand”，将默认键值中的 “Putty.exe” 部分改为 “Putty.cmd” （前后的文字保持不变）。

接下来，我们在 Putty.exe 的文件夹下创建一个 Putty.cmd 文件，编辑其内容为：

> @start %~dp0putty.exe -load &#8220;%~n1&#8221;

现在，再从任务栏图标上点右键，选择其中列出的 .ssh 文件，是不是成功从 Putty 中打开了相应的 session ~

需要注意的是，经过上述修改以后，双击 .ssh 文件不会再自动添加到 Jump List 中，你必须通过拖拽 .ssh 文件到任务栏图标上的方式固定它。然后修改注册表中的 “HKEY\_CLASSES\_ROOTApplicationsPutty.exeshellopencommand” 默认键值，和上面一样将其中的 “Putty.exe” 部分改为 “Putty.cmd” 。

由于 Windows 7 本身的固有行为，将来再固定更多的 .ssh 文件到 Jump List 中后，上述注册表键值会自动还原，所以还必须重复修改一次。（这个暂时没找到一个好的解决办法……）

* * *

**UPDATE: terryice 介绍了一款第三方工具 [Jumplist Extender](http://code.google.com/p/jumplist-extender/)，可以完全随心所以的定义 Jump List，适合不需要通过脚本复杂控制的大部分应用场景~ 强烈推荐~**