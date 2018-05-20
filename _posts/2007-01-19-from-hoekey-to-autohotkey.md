---
id: 188
title: “热键”的极致演绎，从Hoekey到AutoHotkey
date: 2007-01-19T02:43:19+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/01/19/from-hoekey-to-autohotkey/
permalink: /2007/01/19/from-hoekey-to-autohotkey/
dsq_thread_id:
  - "250426831"
  - "250426831"
categories:
  - Computer
tags:
  - AutoHotkey
  - Creative
  - EAX
  - Hoekey
  - Hotkey
  - Live
  - Script
---
　　话说[Hoekey](http://www.bcheck.net/apps/hoe.htm)这个软件我已经用了很长时间，年代久远到实在无从考证。而软件本身的存在早已被我淡忘，只在偶尔重装系统时才会发现，原来它并不是Windows的一部分。

　　回头来细致观察Hoekey，发现它非常符合我对工具软件的审美观：Tiny、Efficient and Creative! 仅仅18k的身段、200k余的内存占用，包罗万象的热键功能…… 我对Hoekey的感觉可以归为“一见钟情”、“相见恨晚”的那一类，甚至会觉得没有Hoekey的IT人生是不完整的。

　　前些天偶然间在水木Desktop版上看到有人提起[AutoHotkey](http://www.autohotkey.com/)（AHK），听名字似乎与Hoekey同属“热键”增强类的工具，于是就饶有兴致的研究了一番。下载时已然觉得数M的AHK显得有些臃肿，再看源码，竟然有近5M！虽然第一印象上就大打折扣，但既然下载了好歹还是要试一试吧。好在主程序只有230k（其它附加的工具和脚本就不小了），第一次启动完后，自动弹出Notepad，打开的是它的配置文件，那种似曾相识的感觉~ 呵呵，看来又是一个可高度定制的热键工具！

　　如果用娇俏可人的小家碧玉来形容Hoekey的话，那么AHK便是那琴棋书画样样精通的大家闺秀了。

<!--more-->　　粗略的看了一下AHK的帮助文件，不禁为其庞大的API库所震慑。AutoHotkey这个名字实在算是谦虚，论功能，AHK早已远远超越Hotkey的范畴。就拿其提供的范例Script为例，比较典型的：

**LiveWindows**: Watch Dialog-boxes in Thumbnail &#8212; by Holomind: This script allows you to monitor the progress of downloads, file-copying, and other dialogs by displaying a small replica of each dialog and its progress bar (dialogs are automatically detected, even if they&#8217;re behind other windows). The preview window stays always-on-top but uses very little screen space (it can also be resized by dragging its edges). You can also monitor any window by dragging a selection rectangle around the area of interest (with control-shift-drag), then press Win+W to display that section in the preview window with real-time updates. 

**Mouse Gestures** &#8212; by deguix: This script watches how you move the mouse whenever the right mouse button is being held down. If it sees you &#8220;draw&#8221; a recognized shape or symbol, it will launch a program or perform another custom action of your choice (just like hotkeys). See the included README file for how to define gestures.

**Easy Access to Favorite Folders** &#8212; by Savage: When you click the middle mouse button while certain types of windows are active, this script displays a menu of your favorite folders. Upon selecting a favorite, the script will instantly switch to that folder within the active window. The following window types are supported: 1) Standard file-open or file-save dialogs; 2) Explorer windows; 3) Console (command prompt) windows. The menu can also be optionally shown for unsupported window types, in which case the chosen favorite will be opened as a new Explorer window.

**Volume On-Screen-Display (OSD)** &#8212; by Rajat: This script assigns hotkeys of your choice to raise and lower the master and/or wave volume. Both volumes are displayed as different color bar graphs.

**Window Shading** (roll up a window to its title bar) &#8212; by Rajat: This script reduces a window to its title bar and then back to its original size by pressing a single hotkey. Any number of windows can be reduced in this fashion (the script remembers each). If the script exits for any reason, all &#8220;rolled up&#8221; windows will be automatically restored to their original heights.

　　其中的任何一个倘若作为独立的工具都可算是非常出色了，实在难以想象他们竟然都是以AHK内置的脚本语言所编写的。简单试用了两天后，我彻底为AHK所折服了，能将一款热键工具演绎到如此程度，实在不单单对得起那230k的身躯，哪怕让我割舍50M内存与之也会毫不犹豫。

　　我只用AHK写了一个简单的脚本，就一举解决了Creative Live!声卡的EAX音效无法通过热键调整的弊端，让这个头疼已久的问题迎刃而解！

`#SingleInstance<br />
#/::    ; Hotkey: Win+/<br />
DetectHiddenWindows, On<br />
IfWinNotExist, ahk_class CT_SMXWND<br />
	Run, "C:Program FilesCreativeSurMix2SurMix2.exe",, Hide<br />
WinWait, Creative Surround Mixer 2, EAX Effects<br />
ControlSend, ListBox1, {Home}, ahk_class CT_SMXWND<br />
Sleep, 100<br />
;WinClose, ahk_class CT_SMXWND<br />
DetectHiddenWindows, Off<br />
` 
  
注：上述脚本暂时只实现了关闭EAX音效，以后有时间再来完成余下的功能，说不定可以实现一个OSD热键控制的EAX选单呢，再说不定还能实现Context-sensitive~ 🙂

　　当然，Hoekey的一些优点还是AHK目前所暂时无法替代的（可能是我的理解程度不足，AHK实在给人有些深不可测的感觉），比如“Hide to tray”，“Kill current process”。所以现下小乔、大乔权且共寄檐下，倒也相安无事。:)