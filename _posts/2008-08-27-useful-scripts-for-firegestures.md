---
id: 450
title: FireGestures的实用脚本
date: 2008-08-27T23:18:49+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=450
permalink: /2008/08/27/useful-scripts-for-firegestures/
dsq_thread_id:
  - "250427842"
  - "250427842"
categories:
  - Internet
  - Software
tags:
  - Fire Gestures
  - Firefox
  - Tab Kit
---
浏览器中，我选择FireFox，因为它有强大的插件框架，可以充分发挥DIY的精神；Firefox的手势插件中，我选择FireGestures，因为它有开放的脚本扩展，可以随意打造你所需要的手势。千万别小看甚至忽视了FireGestures的脚本功能，下面几个脚本将彻底颠覆你对FireGestures的认识！（注：脚本代码均系转载）

<!--more-->

**»快速移除页面中的元素**（[引用来源](http://www.xuldev.org/firegestures/getscripts.php)）

<pre>var node = FireGestures.sourceNode;
node.parentNode.removeChild(node);</pre>

非常实用的功能。是居家旅行，消灭广告，毁尸灭迹的必备武器！
  
巨幅广告、飘悬广告、Flash动画…… 通杀！

友情提示：由于FireGesture手势不能从Flash对象上开始，所以请找一个贴近Flash对象的边缘划出手势，一般可以将Flash所在的容器元素（DIV或SPAN）连带Flash一并干掉。

**»关闭当前标签页并选中左/右侧的标签**（[引用来源](http://www.xuldev.org/firegestures/getscripts.php)）

<pre>var tab = gBrowser.mCurrentTab;
if(tab.previousSibling)
  gBrowser.mTabContainer.selectedIndex--;
gBrowser.removeTab(tab);</pre>

<pre>var tab = gBrowser.mCurrentTab;
if(tab.nextSibling)
  gBrowser.mTabContainer.selectedIndex++;
gBrowser.removeTab(tab);</pre>

尽管Tab Mix Plus/Lite或是Tab Kit都提供了所谓的“关闭标签页后智能切换标签”，但给我的感觉根本谈不上智能，甚至很多时候只能用“弱智”来形容…… 所以，我更倾向于自己掌握关闭标签页后的去向。于是，我在FireGestures中配置了“下左”和“下右”两个动作，分别用来在关闭当前标签页后选中左/右侧的标签。

**»让“在新标签页中打开链接”也能与Tab Kit兼容**（[引用来源](http://www.xuldev.org/firegestures/feedback.php?lang=en&mode=single&n=331#comments)）

<pre>// Open Link in New Tab [Alternative] (Tab in Background)
// Opens a new tab by faking a click on the link.

const IN_FOREGROUND = false;

// Check if it's a link the gesture started from, if yes open link in new tab
if (FireGestures.getLinkURL(FireGestures.sourceNode)) {
  // Create a click event
  var event = document.createEvent("MouseEvents");
  event.initMouseEvent("click", true, true, window, 0, 0, 0, 0, 0,
    // Control key - true to open new tab,
    // else current tab is used
    true,
    // Alt key - unnecessary for this script
    false,
    // Shift key - true to open in new window,
    // or if ctrl is pressed open the tab in
    // foreground, else opened in background
    IN_FOREGROUND,
    false, 0, null);
  // Dispatch the event for the "clicked" link
  FireGestures.sourceNode.dispatchEvent(event);
}</pre>

终于…… 这个困扰我已久的问题，没想到在FireGestures的帮助下解决了！这下Tab Kit终于可以比较完美的自动对新窗口分组了！