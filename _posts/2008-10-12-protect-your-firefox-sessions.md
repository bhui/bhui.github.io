---
id: 485
title: 加强Firefox的会话保护和恢复
date: 2008-10-12T16:37:22+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=485
permalink: /2008/10/12/protect-your-firefox-sessions/
dsq_thread_id:
  - "251388353"
  - "251388353"
categories:
  - Computer
tags:
  - Backup
  - Firefox
  - Session
---
如果你也是像我这样习惯了每次退出时在Firefox中保留大量标签，下次打开继续工作和浏览的“重度会话（Sessions）依赖症”患者。那么你多半也曾有过打开Firefox时突然面对空空荡荡的Firefox窗口而茫然不知所措的经历吧？

导致会话丢失的可能很多，比如Firefox崩溃、电脑异常重启…… 关键的问题是会话中保存了太多对我们来说有价值的信息，一旦丢失，则不仅是记忆的损失，还可能造成精神上的打击。

Firefox的会话恢复机制虽然在大部分时候可以从异常中恢复，但却并不那么可靠。为了对其进行加固，我们可以利用DSynchronize的多重备份功能对会话文件进行重点关照：

<!--more-->首先建立一条同步规则，源路径选择你的“Firefox Profile”文件夹。它一般是“%APPDATA%MozillaFirefoxProfiles”中一个随机名称的文件夹（

[参见MozillaZine的详细解释](http://kb.mozillazine.org/Profile_folder)）。

然后为其设置filter (Inclusion)：“sessionstore.js”，并选上“Do not include subfolders on synchronization”。

为了保存多份备份，在“Backup Change”下选择保存最近备份的次数，比如“5”，其它选项采用默认值即可。

最后，为其设定一个Timer，比如每分钟检查一次。

注：不要选择“Realtime sync”，因为DSynchronize的目前版本（2.30.1）中实时同步尚不支持filter。

<center>
  <a href="http://blog.oasisfeng.com/wp-content/uploads/2008/10/dsynchronize-settings.png"><img src="https://blog.oasisfeng.com/wp-content/uploads/2008/10/dsynchronize-settings-300x235.png" alt="" title="DSynchronize Settings" width="450" /></a>
</center>

完成上述步骤后，你就拥有了一个强力保护加持过的Firefox会话了。倘若遇上会话丢失，先不要慌张，切忌轻举妄动，第一时间坐下来，深呼吸几次，直到情绪稳定。然后关闭Firefox，从上述备份的文件夹中取出最近一份正常的sessionstore.js文件，覆盖回Firefox的Profile文件夹中。再次启动Firefox，丢失的会话就回到你的面前了！ ^_^