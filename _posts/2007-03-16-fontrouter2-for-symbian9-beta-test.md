---
id: 220
title: FontRouter2 for Symbian 9 启动第一轮测试
date: 2007-03-16T21:55:05+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/03/16/fontrouter2-for-symbian9-beta-test/
permalink: /2007/03/16/fontrouter2-for-symbian9-beta-test/
dsq_thread_id:
  - "250427061"
  - "250427061"
categories:
  - Development
  - Symbian
---
发布页面：<a href="http://fontrouter.oasisfeng.com/forum/viewforum.php?f=5" target="_blank">http://fontrouter.oasisfeng.com/forum/viewforum.php?f=5</a>

由于Symbian 9安全机制的限制，所有被Server调用的ECOM插件都必须至少拥有ProtServ权限。为什么有这个限制呢？Symbian 9安全体系的介绍中给出了缘由：

> <p style="margin-left: 18pt; text-indent: -18pt">
>   <span lang="EN-GB"><span>1.<span> </span></span></span><strong><em><span lang="EN-GB">The capabilities of a process never change</span></em></strong><em><span lang="EN-GB">. </span></em><span lang="EN-GB">There is no way of adding capabilities to a process, nor of removing capabilities from a process. All DLL code runs at the capability level of the process that loads it.</span>
> </p>
> 
> <p class="MsoNormal" style="margin-left: 18pt; text-indent: -18pt">
>   <span lang="EN-GB"><span>2.<span> </span></span></span><strong><em><span lang="EN-GB">A process cannot load a DLL with less capability than itself</span></em></strong><em><span lang="EN-GB">.</span></em><span lang="EN-GB"> The need for this constraint follows from the fact that all DLL code runs at the capability level of the loading process and therefore must be at least as trusted at the loading process. DLL capabilities only reflect the level of trust that the loading process can place in them; they don’t actually authorise anything.</span>
> </p>

但就是因为这个机制本身缺陷而强加的约束，使得完全用不到“ProtServ”权限的FontRouter2也无法采用自授权证书方式发布。在这一点上，实在应该对Symbian 9的DLL安全机制设计提出批评，看看在Symbian开发者论坛上因为Recognizer Plugin所面临的同样问题而引发的争论，就可以理解众多Symbian 9开发者的感受了。

言归正传，正是因为上述原因，目前FontRouter2 for Symbian 9只能采用“未认证安装包”的形式发布，它不能被直接安装至手机中。用户必须首先向Symbian Signed申请开发者证书，并使用获得的证书自行对安装包进行授权，才能在手机上正常安装和使用。详细的步骤和注意事项可以参考以下文章：

<span class="postbody"><a href="http://" target="_blank">http://www.gosymbian.com/forum/viewtopic.php?t=757</a> （英文）<br /> <a href="http://blogs.forum.nokia.com/view_entry.html?id=429" target="_blank">http://blogs.forum.nokia.com/view_entry.html?id=429</a> （英文）<br /> <a href="http://bbs.0110.cn/redirect.php?tid=303848&goto=lastpost&frameon=no" target="_blank">http://bbs.0110.cn/redirect.php?tid=303848&goto=lastpost&frameon=no</a> （中文）</span>