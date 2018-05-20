---
id: 205
title: THeapWalk的Symbian 9实现
date: 2007-02-23T21:18:08+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/02/23/theapwalk-for-symbian9/
permalink: /2007/02/23/theapwalk-for-symbian9/
dsq_thread_id:
  - "250426942"
  - "250426942"
categories:
  - Development
  - Symbian
---
　　在移植FontRouter2到Symbian 9的过程中，碰到了一个大难题：THeapWalk这个类彻底的从Symbian 9中消失了！与新版本中其它很多API变化不同的是，THeapWalk类的功能虽然被新的RHeap::Walk()所取代，但该方法已不再从EUser.dll中导出，也就意味着它的身份从此变成了“内部API”，不再对第三方应用开发者开放。

　　THeapWalk是用于测试内存问题的一大利器，其地位难以被取代，如果就此抛弃，实在太可惜了。好在天无绝人之路，经过一天时间的彻底分析，终于让我发现了Symbian为其留下的一个后门。利用以下适配代码，可以在Symbian 9实现对THeapWalk功能的完整模拟，希望对同样遇到移植问题的朋友有所帮助：

<pre>class THeapWalk
	{
protected:
	enum TCellType
	{
		EGoodAllocatedCell, EGoodFreeCell,
		EBadAllocatedCellSize, EBadAllocatedCellAddress,
		EBadFreeCellAddress, EBadFreeCellSize
	};
public:
	THeapWalk(RHeap &aHeap) : iHeap(&aHeap), iValue(0) {}
	TInt Walk()
		{ iHeap-&gt;DebugFunction(RHeap::EWalk, &DoInfo, this); return iValue; }
	virtual void Info(TCellType aType,TAny* aBase,TInt aLength)=0;
protected:
	inline TInt Value() const { return(iValue); }
	inline void SetValue(TInt aValue) { iValue = aValue; }
private:
	static void DoInfo(TAny* aPtr, TCellType aType, TAny* aBase, TInt aLength)
		{ ((THeapWalk *) aPtr)-&gt;Info(aType, aBase, aLength); }
	RHeap* iHeap;
	TInt iValue;
	};</pre>

注：EBadFreeCellSize是Symbian 9新增的一种Cell状态。