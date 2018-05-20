---
id: 300
title: 为WordPress中不同页面搭配独特的Widgets
date: 2008-01-01T12:15:26+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2008/01/01/use-seperate-widgets-set-in-wordpress/
permalink: /2008/01/01/use-seperate-widgets-set-in-wordpress/
dsq_thread_id:
  - "250427650"
  - "250427650"
categories:
  - Internet
tags:
  - Sidebar
  - Widget
  - WordPress
---
有些Widget，如Related Posts，一般来说只应出现在单帖的页面中，而通常首页里大家会习惯堆砌比较多的Widgets，如Twitter、Del.icio.us之类的。WordPress默认并没有给予用户这种便利，而且搜索了一下Plug-in Category似乎也没有找到这样功能的插件，只好自己动手来改造一下。

根据Google到的一些线索发现，其实Widgets机制本身是支持多个Sidebar的，不过大部分的Theme并没有很好的利用这项功能，即使有用到的情况也大多是并排多个Sidebar的用法。于是顺手牵羊，将它略加改造，用于在不同的页面显示不同的Sidebar。分享改造方法如下：

1. 修改Theme下的functions.php，将

<pre>if ( function_exists('register_sidebars') )
  register_sidebar();</pre>

修改为：

<pre>if ( function_exists('register_sidebars') )
{
  register_sidebar(array('name'=&gt;'Sidebar Home',));
  register_sidebar(array('name'=&gt;'Sidebar Single',));
  register_sidebar(array('name'=&gt;'Sidebar Archive',));
}</pre>

2. 修改Theme下的sidebar.php，将

<pre>get_sidebar();</pre>

改为：

<pre>if ( function_exists('dynamic_sidebar')
{
  if (is_home() && dynamic_sidebar('Sidebar Home'));
  elseif (is_single() && dynamic_sidebar('Sidebar Single'));
  elseif ((is_archive() || is_search()) && dynamic_sidebar('Sidebar Archive'));
  else dynamic_sidebar();
}</pre>

3. 然后回到你的首页后，再打开Widgets管理页面，就可以看到3个不同的Sidebar了。现在就来随心所欲的调整Blog在不同页面下的Widgets组合吧！

Tip：未设置的Sidebar将继承Sidebar Home。