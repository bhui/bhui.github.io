---
id: 90
title: Blog URL调整与mod_rewrite
date: 2006-09-04T03:23:20+00:00
author: oasisfeng
layout: post
guid: 'http://blog.oasisfeng.com/2006/09/04/blog-url%e8%b0%83%e6%95%b4%e4%b8%8emod_rewrite/'
permalink: /2006/09/04/blog-url-change-and-mod_rewrite/
dsq_thread_id:
  - "250426158"
  - "250426158"
categories:
  - Development
  - Internet
tags:
  - Internet
  - WordPress
---
　　当初搭建WordPress的时候，懒得去新增二级域名，于是Blog地址是：<http://www.oasisfeng.com/blog> 现在才发现，不光是URL长了一截，就连一些Code不规范的Theme或者插件都自然而然的“假设”你的Blog在根路径（“/”）上。 唉，一念之差……

<!--more-->　　于是决定手动为WordPress挪一下位置，Blog地址于是变成了更“舒适”的：

<http://blog.oasisfeng.com/>

　　但随即问题就来了，访问Google Blog Search上的结果就变成了经典的“404 Not Found”，这个副作用可不是我所希望的。好在之前对mod_rewrite有所了解，当即写了一个.htaccess文件放在blog文件夹下实现“301 Moved Permanently”。实验了一下，结果很奇怪：http://www.oasisfeng.com/blog/及更长的URL都被成功的重定向，但http://www.oasisfeng.com/blog（少了末尾的“/”）却被定向到了匪夷所思的http://blog.oasisfeng.com//home/oasisfeng/oasisfeng.com/blog，无论我怎么调整.htaccess都没有效果……

　　无奈之下，多加了一条额外的修正规则，才算解决了上面的问题。最后的.htaccess文件内容如下：

> # BEGIN 301
> 
> RewriteEngine On
  
> RewriteBase /blog/
  
> RewriteRule ^$ http://blog.oasisfeng.com/ [R=301,L]
  
> RewriteRule ^/home/oasisfeng/oasisfeng.com/blog$ http://blog.oasisfeng.com/ [R=301,L]
  
> RewriteRule ^(.*)$ http://blog.oasisfeng.com/$1 [R=301,L]
> 
> \# END 301 

　　哪位朋友若知个中原委，还请不吝赐教，多谢了！