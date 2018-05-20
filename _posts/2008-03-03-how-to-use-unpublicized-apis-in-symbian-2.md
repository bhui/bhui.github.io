---
id: 304
title: How to use unpublicized APIs in Symbian
date: 2008-03-03T09:14:57+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2008/03/03/how-to-use-unpublicized-apis-in-symbian/
permalink: /2008/03/03/how-to-use-unpublicized-apis-in-symbian-2/
dsq_thread_id:
  - "250427688"
  - "250427688"
categories:
  - Development
  - English
  - Symbian
tags:
  - API
  - dump
  - library
  - rev-engineer
  - Symbian
  - unpublicized
---
<big><big>1. Why are these APIs unpublicized?</big></big>

You can usually find the unpublicized APIs in four ways:

  1. **APIs are written in SDK document, but marked as &#8220;Published Partner&#8221; or &#8220;Internal&#8221;.**
  2. **APIs are declared in header file with corresponding linkable library, but not documented.**
  3. **APIs are dumped from linkable library, but nowhere declared.**
  4. **APIs are exported from dynamic libraries without corresponding linkable library.**

* &#8220;Linkable library&#8221; is a stub library which hold the information required for the linker to link client programs to the correct ordinals to the real dll. In emulator build or Symbian pre-9 toolchain, the linkable library is appeared as **.lib** file, but in target build of Symbian 9 onwards, it is actually a dummy dynamic library of ELF format with extension **.dso**.

<!--more-->For the first case, Symbian declared the &#8220;Rules for API Usage&#8221; as following in SDK document:

> _It is strongly recommended to only use APIs and methods which are classified as PublishedAll. To ensure that your application will work also in future platform releases, using PublishedAll classified APIs and methods is the safest way._
> 
> _If APIs and methods with other classifications are used (which is strongly discouraged), your application might stop working in future platform versions without any notification from Symbian about deprecation, removal or modification of internal or published partner classified APIs and methods._

As a software developer, I can understand the essentiality of API classification, the more APIs published in SDK, the more compatibility restriction must be enforced in future release. &#8220;Published Partner&#8221; is a special case, which means the changes can be made in a managed way by notifying the involving partners. By the way, APIs marked as &#8220;Deprecated&#8221; should never be used unless no more choices, since they are subject to change or be removed in the future release.

For the latter two cases, as APIs are not classified explicitly, they can be either &#8220;Internal&#8221; or &#8220;Deprecated&#8221;. So, use these APIs only when no documented ones are suitable.

The last case is rare and even more dangerous for developer usage. Although in practice, Symbian suggests never breaking the export ordinals of dynamic libraries, the absence of library file implies the possibility of ordinal changes, or even that exports were not frozen. (Please correct my if I&#8217;m wrong)

In conclusion, always prefer the &#8220;Published All&#8221; APIs prior to the unpublicized ones. In case unpublicized APIs are used, never ignore the risk of API changes, thus you should carefully test them on the real phone and all future releases (models).

<big><big>2. Use the undeclared APIs</big></big>

I start to talk about the usage of unpublicized APIs from the third case, as assumed that you can easily handle the first two cases. All files mentioned later are of emulator build (WINS/WINSCW) except for explicitly declaration.

From a article <a href="http://www.newlc.com/How-to-dump-DLL-exports-using-LIB.html" target="_blank">&#8220;How to dump DLL exports using LIB files&#8221;</a> on the famous developer community NewLC.com, you can figure out all the knowledge of dumping exports from library. In practice, when you work on emulator build, I recommend the <a href="http://mikie.iki.fi/symbian/reverse.html" target="_blank">Perl script written by Mika Raento</a>, this script helps generating header file needed by the APIs. On target build of Symbian 9 onwards, the linkable library file is changed to dummy library (.dso) for GNU toolchain, which rendered the old .lib files useless. As a supplement to the article mentioned above, you can use this command to dump exports from .dso file:

<pre>objdump -T euser.dso | c++filt</pre>

Note: Since the demangling style differs between VC and GNU C++ compiler, you can not get the type of return value from the dumped exports of .dso file. This is a mechanism restriction.

In most time, the libraries are present both in emulator and target build, and they are consistent with each other on the exports, although the ordinals are different. (&#8220;Ekern.exe&#8221; is an exception, which exports more APIs in armv5 than in winscw). So you just need to generate the header from emulator build, and use it for both builds without any problem. But you may experience the situation that no corresponding library of target build, especially for the real phone related APIs. In this case, you must rebuild the library manually. I will cover the detailed steps in the next chapter.

<big><big>3. Dig the hidden APIs</big></big>

In some extreme cases, we have only the dynamic library. No headers, no linkable libraries, even the worse, no symbol names (because Symbian only supports exporting by ordinal). How could we discover and use these hidden APIs?

For the first half, discovery of the hidden interface need some disassembly skills. Basically two approaches, analysis the exported functions themselves, or analysis other executables / libraries which imported them. I will not cover the deep details, as that might be a long story far away from this topic. Necessary parts may be mentioned as a hint. Now let&#8217;s go directly into the second half.

As the excutable only need dynamic library for running (dynamic linking), in theory, we just need the dynamic library itself, from which all the rest can be respawned. Since the functions are exported by ordinal, name is not important technically, you can just name the exports a(), b(), c(), and etc, as ordinal grows. But in practice, we all want the accurate name for calling convenience. So, if possible, digging the function or other ones which imported it is a shortcut, hope that you may luckily find the debugging information or calling log text such as &#8220;Call foo() &#8230;&#8221; or &#8220;Enter foo() &#8230;&#8221;. Another tip, exported symbols were generally sorted when library was first released, thus the proximate neighbor symbols can help narrowing the range for name guess. (the sort rule may differs from compiler to compiler) But according to the export freezing mechanism of Symbian, newly introduced functions to a frozen library always add to the last ordinal, which means they don&#8217;t comply with the export sorting. So carefully treat them as an exception. After the symbol names are fixed, although we still need further information about the arguments and returning value in order to reconstruct the interface declaration, let me assume that you can finish it well. (Just another disassembly work with the similar fashion).

Now we have a reconstructed header with interface declarations, it&#8217;s time to make a dummy linkable library. To achieve this goal, generally you have 2 choices.

The first one is easier but may take more time. You create a normal Symbian project with &#8220;TARGETTYPE&#8221; set to &#8220;dll&#8221; and implement all the interfaces defined by the header reconstructed just now with empty function body. Then make and freeze it, you will get the corresponding linkable library. Be sure to double check the frozen .def file for ordinal consistence with original dynamic library. If any ordinal inconsistent, you should review the function name which may be a bad guess, then correct the function name (or modify the .def to force the ordinal fix, personally discouraged) and rebuild it.

The second choice is much more direct, if you are familiar with the format of .def file. Just manually create the .def file with all the pairs of symbol name and ordinal. Then use the tool &#8220;elf2e32&#8221; to generate the linkable library from .def file directly:

<pre>elf2e32 --targetype=implib --definput=foo.def --dso=foo.dso --linkas=foo{000a0000}[10011237].dll</pre>

Note: &#8220;elf2e32&#8221; is only available in Symbian 9 SDK onwards. So you have to use the first method for Symbian pre-9 SDKs.

You have all the materials ready now, just use these APIs like the ordinary ones, and have fun exploring the underhood of Symbian! (:

* * *Revision History:</p> 

2008.3.3 Part I (section 1 and 2) was published.
  
2008.4.9 Part II (section 3) was published.
  
2008.4.13 Two parts were merged, and section 2 was modified to add library dumping for .dso file in Symbian 9 onwards.