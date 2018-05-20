---
id: 179
title: Symbian下的GB2312 / GBK / GB12345 / BIG5中文编码支持插件
date: 2006-12-17T23:02:55+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/12/17/symbian-chinese-charconv/
permalink: /2006/12/17/symbian-chinese-charconv/
dsq_thread_id:
  - "250426716"
  - "250426716"
categories:
  - Symbian
---
　　这是一组为Symbian提供中文简/繁体编码支持的插件，针对N-Gage、N9500等**非中文机型**提供对中文编码的支持（中文机型无需使用），与FontRouter结合使用可以在任何语种的Symbian手机上实现完整的中文显示解决方案。

　　**注：这是Nokia的内部版本，非官方渠道提供，请谨慎使用！本人不对使用该插件造成的任何后果承担责任，下载和使用此插件视同接受本条款。**

　　首先要提到的是tomken，在我找到Nokia的内部版本前，一直使用了两年tomken自己开发的GB2312/GBK/BIG5编码插件，虽然有一点瑕疵（貌似没有实现重入时的双字节的切分处理 = =?），不过其意义在于“从无到有”，可以说没有当年tomken开发的编码插件，就没有完整的N-Gage中文解决方案！当然，Nokia的这个版本完全没有了上述tomken所开发版本的瑕疵，再也不会出现部分段落乱码甚至无法显示（如QReader中）的问题了。

<!--more-->下载地址：


  
<http://fontrouter.oasisfeng.com/archives/ChineseCharconv.rar>

安装方法：
  
　　将所有文件解压缩到C盘或MMC的SystemCharconv下（压缩文件已包含相对路径）。如果希望安装在C盘，请务必先安装在MMC中测试通过后再移至C盘。

注：
  
（1）理论上支持Symbian9之前的所有型号，已在本人的N-Gage上测试通过。
  
（1）部分非中文机型也自带了对中文编码的支持，请检查ROM中systemcharconv下是否已有同名文件，若有则不必安装本插件包。
  
（2）使用GB12345/BIG5编码需要中文字体包含繁体字符集（即通常所说的GBK字体）。