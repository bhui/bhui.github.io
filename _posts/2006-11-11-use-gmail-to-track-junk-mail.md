---
id: 158
title: 用Gmail追踪垃圾邮件的源头
date: 2006-11-11T11:53:45+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/11/11/use-gmail-to-track-junk-mail/
permalink: /2006/11/11/use-gmail-to-track-junk-mail/
dsq_thread_id:
  - "250426619"
  - "250426619"
categories:
  - Internet
tags:
  - Alias
  - Email
  - Gmail
  - Google
  - Junk
  - Spam
---
　　在互联网上的免费服务层出不穷的今天，你是否也曾试用过不少？你可知那些信誓旦旦宣称保护个人隐私的网站可能正是垃圾邮件肆虐的源头。它们将你的Email地址出售给广告商，从而“贴补”其免费服务的支出。

如果你也是一个像我这样用同一Email地址到处试用免费服务的人，那么几乎很难察觉到是哪一个免费服务商“出卖”了你的Email地址。受[《使用圆点来对付Gmail的垃圾邮件》](http://www.cnbeta.com/modules.php?name=News&file=article&sid=17986)一文的启发，我们完全可以借助Gmail提供的[“别名功能”](http://mail.google.com/support/bin/answer.py?answer=12096&topic=1565)将它们“钓”出来并加以单独屏蔽。

假如你的Gmail地址是zhangsan@gmail.com，那么在注册不同的免费服务时，可以使用相应的别名（注意在别名前用统一的前缀），如：
  
zhangsan+for.baidu@gmail.com
  
zhangsan+for.yahoo@gmail.com
  
zhangsan+for.maxthon@gmail.com
  
&#8230;&#8230;

然后我们可以在Gmail中创建一条过滤规则（to:zhangsan+for），为所有包含该类别名的邮件贴上标签，这样就能轻松逮到垃圾邮件的罪魁祸首了。

注：有些邮件系统可能并不能识别&#8221;+&#8221;这个符号,这样就会导致你无法收到它们的邮件.