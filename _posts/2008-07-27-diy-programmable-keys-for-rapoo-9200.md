---
id: 371
title: DIY雷柏9200的16个可编程按键
date: 2008-07-27T22:51:52+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=371
permalink: /2008/07/27/diy-programmable-keys-for-rapoo-9200/
dsq_thread_id:
  - "250427824"
  - "250427824"
categories:
  - Computer
tags:
  - AutoHotkey
  - Rapoo
  - 可编程
---
今天入手了雷柏9200无线鼠标，因为在这个价位中，它提供了绝对有竞争力的“8按键”+“二维滚轮”。再加上双模式的切换和滚轮，总共可以使用多达19个功能键！

但遗憾的是，纵然拥有如此多的按键，但官方所提供的驱动程序却只能支持对其中仅仅两个按键定制功能，不能不说是完全埋没了9200的天赋……

好在DIY精神就是要突破限制，明知不可为而为之！利用AutoHotkey，我们可以实现对其中最多16个键的功能随心定制，充分发挥你无边无际的想象力和炉火纯青的弹指神功！

<!--more-->经过分析，在标准模式（办公模式）下，拇指位的两个键分别是Windows标准的“第四”和“第五”鼠标键，与其它大部分鼠标一致。而“放大/缩小”两个键在安装驱动前是没有作用的，而雷柏的驱动程序固定将其模拟为“Ctrl+滚轮”，即常见软件中的缩放功能。

当切换到多媒体遥控模式后，除基本的左右键和水平滚轮外，其它按键均被赋予新的作用：拇指位的两个键现在等同于多媒体键盘上的“上一曲”和“下一曲”按钮，而原本的两个缩放键则分别产生“播放/暂停”和“启动播放器”两个功能，也是多媒体键盘上常见的功能键之一。鼠标纵向滚轮则成为了“音量调节”，按下滚轮是“静音”。

通过以上分析，我们很容易找到上述全部16个可编程按键在AutoHotkey中对应的按键名称：

<pre>【通用】
左键：LButton
右键：RButton

【办公模式】
中键：MButton
滚轮向上：WheelUp
滚轮向下：WheelDown
拇指上：XButton2
拇指下：XButton1
缩小：^WheelUp
放大：^WheelDown

【遥控模式】
静音（中键）：Volume_Mute
音量增大（滚轮向上）：Volume_Up
音量减小（滚轮向下）：Volume_Down
下一曲（拇指上）：Media_Next
上一曲（拇指下）：Media_Prev
播放/暂停：Media_Play_Pause
启动播放器：Launch_Media</pre>

“CPI”键由于只是控制鼠标自身状态，并不与电脑交互，所以是无法定制的。而水平滚轮由于AutoHotkey本身无法支持，所以也暂时不能实现定制。

需要特别说明的是，“放大/缩小”两个按键的效果是依靠雷柏的驱动程序模拟“Ctrl+滚轮”产生的，因此如果直接在AutoHotkey中简单重映射^WheelUp和^WheelDown的话，则会导致如果真正用“Ctrl+滚轮”也会被拦截，无法手动进行缩放操作。解决的办法是使用AutoHotkey的物理按键状态判断功能：

<pre>$^WheelUp::
If GetKeyState("Ctrl", "P") = 0
  MsgBox ZoomIn ; Replace it with whatever you want.
else
  Send ^{WheelUp}
return

; Zoom Out
$^WheelDown::
If GetKeyState("Ctrl", "P") = 0
  MsgBox ZoomOut ; Replace it with whatever you want.
else
  Send ^{WheelDown}
return</pre>

仅以此文献给各位“雷友”，让你真正成为手中鼠标的主宰！