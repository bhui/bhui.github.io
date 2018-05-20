---
id: 219
title: 我“芯”未老
date: 2007-03-23T21:34:47+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/03/23/overclock/
permalink: /2007/03/23/overclock/
dsq_thread_id:
  - "250427050"
  - "250427050"
categories:
  - Computer
tags:
  - ASUS
  - Athlon64
  - ClockGen
  - H.264
  - K8N
  - nForce3
  - nVidia
  - Overclock
---
<p dragover="true">
  在最近HDTV/HDRip汹涌大潮的席卷下，我的旧电脑已倍感不支。一遇到高码率的H.264电影，音画异步的状况常常是惨不忍睹。好在当年攒这台电脑时亦预见到了今日可能面临的困境，潜藏在CPU深处的那股超频异禀也终于盼到了大展宏图的这一天。
</p>

<p dragover="true">
  当初刚买这台电脑时，为了不致辱没我“超频狂人”的称号，虽需求并不强烈，但也小超了一点。Athlon 64 2800+的CPU在225的外频下一跑就是两年。千里伏骥，唯仰天嘶鸣，实在委屈它了……
</p>

华硕K8N 这块主板虽然在超频界并不被看好，但既然到了我的手中，那也绝非池中之物。三压分调、外频双锁，再加上过频保护的金钟罩，上手的分量可谓恰到好处。

闲话不多说，直接来看超频的成果吧：

3850+ (275 x 9, DDR333 @ 458 & 1T, HT 3x @ 825) 稳定
  
3920+ (280 x 9 @ 1.6V, DDR333 @ 466 & 1T, HT 3x @ 840) 稳定
  
4060+ (290 x 9 @ 1.6V, DDR333 @ 482 & 1T, HT 3x @ 870) 进入WinXP，播放H.264片刻后死机
  
4100+ (295 x 9 @ 1.6V, DDR333 @ 491 & 1T, HT 3x @ 885) 能点亮，但无法进入WinXP

上述实验充分展现了这块Athlon64的超频潜力，总算不枉当年花的大价钱了。在电压方面，我还是比较怜惜，只加了0.05V，毕竟夏天的脚步已悄然临近了；另一方面，本着追求性能平衡的理念，我没有打算通过牺牲内存和HT的频率来换取CPU“一枝独秀”。

最终，经过几天时间的考验，锁定“3920+”为最佳的稳定频率，基本实现了绝大多数码率的H.264正常播放。:)

<p dragover="true">
  不过问题也随之而来了，首先是发热量，以往通过“Cool&Quiet”的调控，CPU风扇几乎未曾全速运转过，但现在只要CPU稍显繁忙就会听到风扇匆匆提速的脚步声；与此同时，能耗明显增加，特别是夜间下载的时候，颇为浪费。
</p>

<p dragover="true">
  于是，寻找一条平衡性能与能耗的道路就显得非常迫切了，浮现在我脑海中第一个念头就是“软超频” —— 一个曾经叱诧风云却渐已被人淡忘的名词。以往，“频随芯动”的境界只有在AMD或Intel施展独门秘传的绝技时才能有幸得见，但借助“软超频”，我们已然可以任意驾驭这种上乘心法，在泰山压顶时施展出雄浑内力，在凌波微步间轻扬起拂柳之袖。
</p>

<p dragover="true">
  下面就祭出我所使用过的传说中软超频的“七种武器”，挨个掂量掂量。
</p>

<p dragover="true">
  <a href="http://www.nvidia.com/object/sysutility.html" title="nVidia nTune">nVidia nTune</a><br /> 师出武林正宗，可惜学艺不精，眼高手低。<br /> 在调节HT-multiplier，调节CPU外频或AGP频率时常常死机。
</p>

<p dragover="true">
  <a href="http://www.xtremesystems.org/forums/showthread.php?threadid=37345" dragover="true" title="A64Tweaker">A64Tweaker</a> 0.31/0.6beta<br /> 无师自通的武学天才，精通内存调教之术。可惜中道颓丧，缺乏应变乏术。<br /> 完全没有正确识别出nForce3 Pro的内存参数来。
</p>

[A64Info](http://www.xtremesystems.org/forums/showthread.php?t=96678 "A64Info")
  
与A64Tweaker有着极深的渊源，武艺一脉相承，青出于蓝而甚于蓝。
  
最求极致的性能是他的拿手好戏，可调节的内存参数让人眼花缭乱。

[ClockGen](http://www.cpuid.com/clockgen.php "ClockGen") 1.0.5.3
  
系出名门，秉承师门戒律，只修行纯正内功，不屑于旁门左道。
  
仅限调节CPU外频、AGP频率。

[ClockGen for nVidia nForce3 1.04](http://www.robov.elektro.szm.sk/ClockGen-NVNF3.zip "CG-NVNF3")
  
与ClockGen为同门师兄弟，但学艺泛而不精。
  
功能部分有效，可调节FID、调节VID无效、调节CPU外频或AGP频率时死机。

[ATI Tool](http://www.techpowerup.com/atitool/ "ATI Tool")
  
ATI显卡的软超频工具，地位无可动摇。与CPU软超频堪称“双剑合璧”！

[HoeKey](http://www.bcheck.net/apps/hoe.htm "Hoekey")
  
这不是那个小巧强悍的热键工具么？没错！它的“指点”，再加上ClockGen for nForce3，那才真正发挥出了软超频的精髓！正所谓“笑看风云，尽在弹指一挥间！”。