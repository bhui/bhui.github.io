---
id: 113
title: HBufC使用中的陷阱与误区
date: 2006-09-16T18:56:29+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2006/09/16/trap-and-misunderstanding-of-hbufc/
permalink: /2006/09/16/trap-and-misunderstanding-of-hbufc/
dsq_thread_id:
  - "255304369"
  - "255304369"
categories:
  - Development
  - Symbian
tags:
  - Symbian
---
　　Symbian是为资源高度受限的手持终端所设计的，所以应用开发中须要时刻保持这样的警觉。Symbian默认为应用程序创建的栈区是较小的，因此在栈中创建缓冲区时应当特别小心。

　　虽然Symbian SDK中也提供了TBuf、TBufC等可用于栈的缓冲区描述符，但一般仅限用于小缓冲区。对于大缓冲区，推荐的作法是使用HBufC类在堆中创建缓冲区描述符。接触过HBufC类的朋友一定会觉得非常奇怪，为什么没有一个对应的“可修改(Modifiable)”的HBuf类呢？这个问题还真不容易解释，引用[《Symbian Explained: Effective C++ Programming for Smartphones》](http://blog.oasisfeng.com/2006/08/24/symbian-os-explained-effective-c-plus-plus/)一书中的说法：

<!--more-->

> 　　通常我们都觉得应该有一个HBuf类存在，以便与TBuf类相对应。事实上，假如这个HBuf类存在，则我们必须为其考虑长度的自动扩充以及内存管理的一系列问题。但Symbian中描述符体系旨在被设计为高效而不负责内存管理（由程序员去考虑内存的管理），而如果有这样一个“可修改”的HBuf类却没有自动扩充机制，这会让人觉得很古怪。

　　所以，我们不得不用一个“不可修改(Unmodifiable)”的HBufC类来作为当缓冲区，这似乎让人觉得越发别扭了（其实我宁愿选择有一个长度固定的HBuf可用 🙁 ）。那么我们应该如何正确的使用HBufC类呢？其实，这里面存在的陷阱和误区恰恰是人们认为理所当然的那一面。

（1）HBufC的分配

　　标准的作法是：HBufC::NewL 或 HBufC::NewLC，但有些时候，我们还有一个更高效的选择，例如当需要创建一个HBufC来保存另一个描述符的内容时：
  
`<br />
void CExample::SaveDataL(const TDesC& aData)<br />
{<br />
  iBuffer = HBufC::NewL(aData.Length()); // HBufC CExample::iBuffer<br />
  TPtr ptr(iBuffer->Des());<br />
  ptr.Copy(aData);<br />
  ...<br />
  // 应当替换为下面这一行（更高效）<br />
  iBuffer = aData.AllocL();<br />
}<br />
` 

（2）HBufC用作TDesC

　　按照Symbian描述符体系的惯性思维，常常有人会想到使用HBufC::Des()来达到这个目的。但这样不仅实现过程冗余，而且还浪费了12个字节的栈区。正确的方法其实很简单，我们只需要一个“*”：
  
`<br />
const TDesC& CExample::GetData(void)<br />
{<br />
  return(*iBuffer);<br />
}<br />
` 

（3）HBufC用作TDes

　　你或许会问，这下我用HBufC::Des()总不会有问题了吧？方法确实没错，不过，最大的陷阱就在这里！

　　HBufC是一个“不可修改”的描述符，它的实际内存布局中头部只含有一个表示“长度”的TUint。那么构造TDes所必需的另一个元素“最大长度”从哪里来的呢？在这个问题的处理上，Symbian用了一点小小的技巧（编程中的trick往往都是灾难的罪魁祸首……）。**TDes的“最大长度”其实是从HBufC所占据的这块内存区间的“分配单元描述(Heap Cell Struct)”（分配内存单元时记录分配信息的头部结构）中获得的，而这样得到的“最大长度”常常是大于我们用HBufC::NewL()创建缓冲区时填写的长度！！！**这是因为实际分配的内存大小是以某个粒度大小对齐的，如果当初创建缓冲区时的指定大小不是这个粒度的整倍数则会导致HBufC::Des()构造的描述符最大长度超出我们的预期。例如以下代码：
  
`<br />
TBool CExample::FindL(TDes& aData)<br />
{<br />
RFile file;<br />
buffer = HBufC::NewL(KMaxBufferLength);<br />
TPtr ptr = buffer.Des();<br />
...<br />
file.Read(ptr);<br />
aData.Copy(ptr);<br />
}<br />
` 

　　如果传入aData的最大长度也是KMaxBufferLength，那么通常都没有人会想到这个函数也会发生Panic吧？实际上，RFile::Read()按照ptr的最大长度读取文件，那么buffer中保存的数据很可能已经超过了KMaxBufferLength，下面再Copy到aData中时就会导致Panic &#8211; USER 11。