---
id: 273
title: 写了一个方便签名SIS文件的小工具
date: 2007-09-20T02:18:46+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/09/20/quick-signing-tool-for-symbian/
permalink: /2007/09/20/quick-signing-tool-for-symbian/
dsq_thread_id:
  - "250427569"
  - "250427569"
categories:
  - Symbian
tags:
  - Sign
  - signsis
  - Symbian
  - 签名
  - 证书
---
用批处理写的，需要Win2000以上的扩展命令行支持（默认开启）。

【下载地址】

http://fontrouter.oasisfeng.com/archives/sign.bat

【安装方法】

（1）将sign.bat文件放在任意位置，同时将你的证书文件和Key文件也放在同一位置（这一对文件的文件名必须相同，比如E90.cer和E90.key）
  
（2）如果你没有安装Symbian SDK，那么你需要弄到一个signsis.exe文件，放在同一文件夹下（由于版权的关系，这里不提供此文件）
  
（3）如果你的证书文件含有密码，请修改sign.bat文件，在第三行set PASSPHASE=后面写上你的密码（不能含有空格）
  
（4）为sign.bat创建一个快捷方式，拖到快捷工具栏（或者桌面上）

【使用方法】

签名单个文件：直接将需要签名的文件拖放到快捷工具栏（或桌面）的快捷方式上即可
  
签名多个文件：将文件夹拖放到快捷工具栏（或桌面）的快捷方式上即可

签名后的文件存放于子文件夹signed下。文件名形如“FontRouter.**signed.for.E90**.sis”（粗体部分是自动添加的，for后面的内容与证书文件名一致）。

注： 如果需要同时为多个证书签名，可以在sign.bat的文件夹下放置多对证书/Key文件，每一对的文件名相同。这样每次签名就会为它们各生成一份签名后的sis文件。