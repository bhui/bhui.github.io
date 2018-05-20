---
id: 235
title: Explore and Hack the Server Heap in Symbian
date: 2007-04-26T01:02:36+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/04/26/explore-and-hack-the-server-heap-in-symbian/
permalink: /2007/04/26/explore-and-hack-the-server-heap-in-symbian/
dsq_thread_id:
  - "250427250"
  - "250427250"
categories:
  - Development
  - English
  - Symbian
tags:
  - ECOM
  - Heap
  - Open-Font-System
  - plug-in
  - Server
  - Symbian
  - THeapSearch
  - THeapWalk
---
One of the most important design in Symbian is the well-known server/client framework. As the server and client are in different process spaces, hacking the server is generally difficult to achieve by means of normal application. But another important framework provided by Symbian give us a chance, the Plug-in framework, which is also merged into the ECOM framework in newer Symbian OS.

<!--more-->Take the Open Font System interface for example, any OFS plug-in installed in Symbian is actually loaded by Font and Bitmap Server at system start-up. Thus they are running just in the same process space of Font and Bitmap Server. So if you want to hack the server, you should first find the right key &#8211; the corresponding plug-in interface of that server. Not all servers have a plug-in interface, but the plug-in mechanism is so popular and you can find it in most of the common servers.

After breaking the door of server, we could still see nothing in the dark room. What we need now is a lamp, which can help us find the right things. Fortunately there **is** a lamp that could even light up all the corners of server heap. But how could you imagine such a powerful tool was even forgotten by people and only be treated as a part of the ordinary debug kit? OK, no more superfluous words, let me introduce the amazing lamp &#8211; class THeapWalk. It will walk through all the cells in the specified heap, and pass each one to the virtual function. We just need to identify each given cell and find out the cookie. As a restriction in Symbian, RTTI is not supported (in pre Symbian 9, and also not recommended in Symbian 9), but we could still simulate the typeid() for all CBase derived classes by extracting the pointer of virtual function table.

Some more words here, the address of allocated cells in heap are not the address of corresponding objects. Actually there is a small piece of cell header which keeps the information of cell length and pointer to next cell, in the beginning of each heap cell. The real object resides just behind its cell header.

**Tip:** For compatible reason, never assume that the length of cell header to be sizeof(RHeap::SCell), use a live constructed object and RHeap::GetAddress() to figure out.

Now, let&#8217;s do a small wrap and help our Cinderella wear her glass slippers. (:

<pre>class THeapSearch : private THeapWalk
{
public :
	THeapSearch(RHeap& aHeap);
	TInt Search(CBase & aRefObject);
	inline CBase * FirstResult() { return iObjectFound; }
	// Override this function to deal with each object found.
	virtual void DealL(CBase * /*aObject*/) {}
private:
	void Info(TCellType aType,TAny *aBase,TInt aLength);
	RHeap & iHeap;			// The heap to search object in.
	CBase * iObjectFound;		// Object found (NULL if not found)
	CBase * iRefObject;		// Reference object
	TInt iCellLengthExpected;	// Expected length of cell
	TInt iCellHeaderLength;		// Length of cell header in current build
	TInt iTypeId;			// Address of virtual function table
};</pre>

_Detailed implementation is omited and can be found here: [[Heap Search Code Snippet]](http://blog.oasisfeng.com/wp-content/uploads/2007/04/heapsearch.txt "Heap Search Code Snippet")_

Finally, we have all the essential bases ready for an exciting &#8220;Server Heap Tour&#8221;, and I will demonstrate the process by hacking our innocent CFontStore object of Font and Bitmap Server to change the default font render effect to enjoyable &#8220;Anti-Aliased&#8221;. (Only available on Symbian 7 and later, because Symbian 6 has no anti-aliased bitmap type support.)

<pre dragover="true">CFontStore * font_store = NULL, * ref = CFontStore::NewL(& User::Heap());
THeapSearch heap_search(User::Heap());
&lt;cbase>if (1 == &lt;/cbase>heap_search.Search(* ref&lt;cbase>)&lt;/cbase>&lt;cbase>&lt;/cbase>&lt;cbase>)
{
    &lt;/cbase>font_store = reinterpret_cast&lt;CFontStore *&gt;(heap_search.FirstResult());
    if (font_store)
&lt;cbase>        font_store-&gt;SetDefaultBitmapType(EAntiAliasedGlyphBitmap);
}
delete ref;&lt;/cbase></pre>

Note: Symbian 9 has striped away the THeapWalk class in the SDK, visit my blog and get a working simulation version of class THeapWalk in Symbian 9:
  
 <http://blog.oasisfeng.com/2007/02/23/theapwalk-for-symbian9/>

* * *

<address>
  This article was also posted under <a href="http://www.newlc.com/-Security-.html">NewLC.com &#8211; Tutorial &#8211; Security</a>.
</address>