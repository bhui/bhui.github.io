---
id: 110
title: 从POST到Linux的一体化远程控制
date: 2006-09-18T22:40:29+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/18/remote-control-from-post-to-linux/
permalink: /2006/09/18/remote-control-from-post-to-linux/
dsq_thread_id:
  - "250426258"
  - "250426258"
categories:
  - Computer
  - Linux
tags:
  - AMI
  - KVM
  - Linux
  - Remote-Access
  - Serial-Redirection
---
　　在上次[初尝Remote KVM甜头](http://blog.oasisfeng.com/2006/09/05/diy-remote-kvm-server/)的基础上，本着充分挖掘其实用价值的考虑，最近对这一技术又进行了深入的研究和尝试。

　　在网上查阅了各种相关资料后，才知道上次所实现的串口终端功能的正式学名叫做“SREDIR (Serial Redirection，串口重定向)”，它是AMI在其最新的AMI BIOS 8系列中引入的一项新技术，可以看作是一个简化版的“Remote KVM”。主要实现了对字符界面显示输出及键盘输入的重定向到串口，它对于服务器群或者Blade Server来说是非常实用的功能。

　　下面就让我来介绍一下如何利用这项技术实现从POST到Linux的全程串口控制。

<!--more-->　　（1）首先，需要接上普通的终端，并在AMI BIOS的CMOS设置中“Advanced Settings”页下打开“Remote Access”的选项（如果你的BIOS是默认开启该选项的，那么你甚至不必准备一套普通的终端，直接从下一步开始）。

[<img id="image116" alt="CMOS Setup - Serial Redirection" src="https://blog.oasisfeng.com/wp-content/uploads/2006/09/sr_setup.jpg" />](http://blog.oasisfeng.com/wp-content/uploads/2006/09/sr_setup.jpg "CMOS Setup - Serial Redirection"){.imagelink}

　　根据实际情况配置好端口、参数及终端的模式：

　　“Redirection after BIOS POST”应选择“Always”，以保证从POST、Boot Loader到Linux的平滑过渡；
  
　　“Terminal Type”建议选择“ANSI”，这样显示效果最接近实际终端，也能获得最大的兼容性；
  
　　“VT-UTF8 Combo Key Support”建议打开，这样可以使用扩展的F5-F12映射键，这或许在进入某些第三方的Addon ROM时需要用到。

　　（2）完成上述设置后就可以在另一台电脑上通过串口线连接至我们需要控制的服务器，然后打开你的终端程序（Windows自带的“超级终端”即可），匹配好端口参数。一些就绪后，复位服务器，顺利的话，你就可以从终端程序里看到BIOS自检过程的显示信息了。如果没有任何显示或者出现杂乱的信息，那么请检查端口及参数是否匹配。

　　（3）先让我们来试试从远程终端进入CMOS设置，“Del”是通常进入的CMOS设置界面的热键。但问题就在这里，终端程序的键位映射中一般是没有Del键的，你在终端按下Del键实际传到串口的可能就是Ctrl+H或者其它某个（组合）键了。那么如何才能进入CMOS设置界面呢？按照AMI官方文档的说明是可以用另一个替代热键F4来达到相同的作用，但我实际实验发现在我们这块Intel的服务器板上按F4却没有任何效果…… 后来折腾了半天，总算让我找到了另一个替代的办法：在“超级终端”的“连接属性”设置中有一项“Backspace键发送”，把它改为“Del”。这样在POST阶段按下终端的Backspace键就可以成功进入CMOS设置界面了。:)

　　（4）接下来，我们要进一步实现Boot Loader的串口控制。

　　如果你的Boot Loader是字符界面的，而且前面CMOS设置中“Redirection after BIOS POST”选择了“Always”，那么通常你通常可以直接在POST结束后从终端上看到Boot Loader界面了。倘若你不幸和我一样用了图形界面的GRUB，那么此时从终端上是看不到任何显示的（但是你仍然可以“盲打”）。

　　为了解决这个问题，我们需要修改GRUB的配置文件（通常是/boot/grub/menu.lst），注释掉“gfxmenu”所在的一行。这样就可以让GRUB回归到传统的字符界面了。

　　如果到这里你还不能从终端看到Boot Loader的话，那么可能是你的Boot Loader与BIOS的Remote Access存在冲突。你需要手动在GRUB的配置文件中添加下面几行：

<pre>serial --unit=0 --speed=9600 --word=8 --parity=no --stop=1
terminal serial</pre>

　　注：unit参数是串口的序号，0代表COM1，1代表COM2，…… 其它参数需要与CMOS中的配置及终端配置保持一致。

　　（5）而后，我们还必须解决Linux启动过程的串口控制，否则Boot Loader开始加载Linux之后我们就彻底从串口失去控制权了。

　　首先，需要从Boot Loader中去掉任何Splash画面的设置，比如GRUB的配置文件中包含“splashimage”的那一行。然后，在内核参数中增加以下内容：

<pre>console=tty0 console=ttyS0,9600n8</pre>

　　其中，ttyS0代表COM1口，如果你使用的是COM2，那么需要修改为ttyS1。后面的9600n8即串口的参数，应与前述设置保存一致。

　　注：多个console参数存在时，只有最后一个console指定的终端具有交互权，其它终端上只是同步输出启动阶段的信息。所以这里一定要将串口作为最后一个console参数，我们才能从这里登录。

　　OK，万事俱备，让我们从串口登录到Linux吧。怎么？你的root帐号无法登录？对了，还有最后一点忘了说。默认情况下，login程序没有把串口列为安全终端，也就是说，你无法从串口登录root帐号。那么，如何让login建立对串口的信任呢？只需要简单的修改一下/etc/securetty文件，增加一行你的串口设备名，如“ttyS0”即可。

　　以上，我们就完成了全部串口控制所需的步骤，结合上次例子中提到的终端服务，即可轻松实现从POST到Linux的一体化远程控制了。

　　参考资料：“AMI BIOS 8 &#8211; Serial Redirection”: http://www.ami.com/support/doc/AMIBIOS8-SerialRedirection.pdf