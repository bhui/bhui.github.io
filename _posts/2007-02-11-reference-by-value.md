---
id: 199
title: 引用的“按值传递”（Reference by Value）
date: 2007-02-11T22:22:19+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/02/11/reference-by-value/
permalink: /2007/02/11/reference-by-value/
dsq_thread_id:
  - "250426881"
  - "250426881"
categories:
  - Development
  - Symbian
---
　　学习Symbian编程的过程，也是一个升华对C++精髓理解的过程。Symbian的开发模型中用到了数不胜数的C++高级特性，执着于“力求甚解”的话，将会对C++有一个更深层次的认识。

　　我们知道C++从C演变而来，虽然仍旧保留了指针这个可怕的“祸端”，但“引用（Reference）”的出现让人们在最大程度上避免了与指针的直接接触，从而可以更加安全的使用对象。指针的可怕之处在于其“不确定”的指向，而“引用”的本质就是对指针的封装，从而将不确定性拒之于门外。

　　作为一个C++程序员，你可能会抱怨：“我没办法像Java那样忽略指针的存在，有时候除了指针我别无选择……” 那么就让我们来看看指针是否真的无法替代？举两个最常见的困惑：

<li dragover="true">
  我的对象并非一开始就存在，它将在某个必要的时刻才被创建，所以空指针可以为我填补这之前的空白。
</li>
<li dragover="true">
  在某些无法传递引用的场合，比如函数变参，迫不得已用指针代替引用。
</li>

<!--more-->　　第一种场景通常可借助于优化对象关系而消除，设计模式中也提供了一种化解空指针的模式——“Null Object Pattern”。本文主要讨论第二种场景，如何传递“引用”。

　　前面已经提到，“引用的本质是对指针的封装 ”，那么当引用无法被直接传递的时候，我们就需要自己来做这个封装的工作——构造一个“值式引用（Reference by Value）”。

　　来看看Symbian中的实现：

`template <class T><br />
class TRefByValue<br />
{<br />
public:<br />
　　inline TRefByValue(T& aRef) : iRef(aRef) {};<br />
　　inline operator T&() { return(iRef); }<br />
private:<br />
　　TRefByValue& operator=(TRefByValue aRef);<br />
private:<br />
　　T &iRef;<br />
};`

　　模板类TRefByValue定义了public的构造函数和private的赋值运算符，所以它在创建后就不能被改变， operator T&()定义了函数运算符，以实现从TRefByValue还原到引用。以printf类型的变参函数为例：

`static void MyClass::Printf(TRefByValue<const TDesC> aFormat, ...)<br />
{<br />
　　Const TDesC format = aFormat();<br />
　　......<br />
}`

int main()
  
{
  
　　TInt result;
  
　　&#8230;&#8230;
  
　　_LIT(KFormat, &#8220;Result: %d&#8221;);
  
　　MyClass::Printf(KFormat, result);
  
}

　　在MyClass::Printf()的调用过程中，KFormat作为 TRefByValue<const TDesC> 类型被传递，在函数体中再被还原为引用，从而实现了引用的“按值传递”。