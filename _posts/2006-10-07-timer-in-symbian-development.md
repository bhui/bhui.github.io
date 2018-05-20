---
id: 129
title: Timer in Symbian Development
date: 2006-10-07T11:01:56+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/10/07/timer-in-symbian-development/
permalink: /2006/10/07/timer-in-symbian-development/
dsq_thread_id:
  - "250426442"
  - "250426442"
categories:
  - Development
  - Symbian
tags:
  - Development
  - Symbian
  - Timer
---
**（1）TTime::HomeTime() / TTime::UniversalTime()**

　　最常见的时间获取手段，精度不高；因涉及一定的运算过程，效率较低。适用于需要以常规“年月日时分秒”方式使用时间的场合。在EKA2平台下，其精度与低阶系统时钟（Nanokernel Timer）一致，通常为微妙级别。通过 HAL::Get(HAL::ENanoTickPeriod, result) 可以获的具体精度。
  
　　注意：它们使用的是系统时间，这是可以被其它进程修改的。

**（2）User::TickCount()**

　　传统的Tick计数器，精度通常仅为1/64秒（可能随硬件有差异），适用于精度要求较低的场合。通过 HAL::Get(HAL::ESystemTickPeriod, result) 可以获得具体精度。
  
　　注意：在休眠（Standby）状态下，TickCount将停止计数，所以**User::TickCount()在休眠状态下将“损失”计时！**

**（3）User::NTickCount()**

　　低阶系统时钟（Nanokernel Timer），通常提供微妙级Tick。通过 HAL::Get(HAL::ENanoTickPeriod, result) 可以获得具体精度。
  
　　注意：Symbian OS 6.x 没有此API。与TickCount不同的是，User::NTickCount()在休眠状态下不“损失”计时。

**（4）User::FastCounter()**

　　返回值类似于Tick，提供Symbian OS所能支持的最高精度，通常比TTime::HomeTime()更准确。（如果硬件不支持high resolution timer，则毫秒级时钟替代）而且，因为它采用快速的exec call读取一个硬件寄存器的数值，效率很高。通过 HAL::Get(HALData::EFastCounterFrequency, result) 可以获得其具体精度。
  
　　注意：在每次终端从休眠状态激活后，它将同步至正确的数值，也就是说User::FastCounter()在休眠状态下其实也是不“损失”计时的。

　　另外，User::After(), CPeriodic也会在休眠状态下“损失”计时，所以在手机这种特殊的应用环境中，需要特别注意不同定时器在“休眠”状态下计时的差异。