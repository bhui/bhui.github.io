---
id: 272
title: Open Font Rasterizer in Symbian 9
date: 2007-09-13T02:34:12+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/09/13/open-font-rasterizer-in-symbian-9/
permalink: /2007/09/13/open-font-rasterizer-in-symbian-9/
dsq_thread_id:
  - "250427523"
  - "250427523"
categories:
  - Development
  - English
  - Symbian
tags:
  - Font
  - OFS
  - Symbian
---
In the great changes of Symbian 9, most plug-in interfaces have been migrated to ECOM framework, Open Font Rasterizer (OFS for short) interface is just one of them.

Even from the newest SDK document of Symbian 9.2, the OFS related contents are still only for implementation before version 9. The following changes must be considered if you are writing OFS plug-in or porting it to Symbian 9.
  
<!--more-->

  1. As all other applications, the UID of pre-Symbian 9 is no longer available in Symbian 9, you must apply for a new one if you are porting your old OFS plug-in. Please remember, you should use separate UIDs for pre-Symbian 9 and Symbian-9 releases because they are incompatible with the Symbian version of each other.
  2. As migrated to ECOM framework, the ordinal 1 of exported functions needs to be the group proxy for your ECOM plug-in. The formerly exported factory function CMyFontRasterizer::NewL should be keeped unexposed now and only proxied by exported implementation group proxy.
<pre>class CMyFontRasterizer : public COpenFontRasterizer
{
public:
  /*IMPORT_C*/ static COpenFontRasterizer* NewL();
  ...
}

const TImplementationProxy ImplementationTable[] =
{ IMPLEMENTATION_PROXY_ENTRY(KUidMyFontRasterizer, CMyFontRasterizer::NewL) };

EXPORT_C const TImplementationProxy * ImplementationGroupProxy(TInt& aTableCount)
{
  aTableCount = sizeof(ImplementationTable) / sizeof(TImplementationProxy);
  return ImplementationTable;
}</pre>

  3. Because of the scalable-UI introduced in Symbian 9, OFS interface now has two new virtual functions which need to be implemented in your plug-in:
<pre>COpenFontFile::GetNearestFontToDesignHeightInPixelsL()
COpenFontFile::GetNearestFontToMaxHeightInPixelsL().</pre>

The first one is as the same as former COpenFontFile::GetNearestFontInPixelsL(), which is no longer called by OFS framework. The second one just has one more argument &#8220;aMaxHeight&#8221;, which means your plug-in must do the best to find a typeface that fits within the max height, otherwise, a leave must be performed. If aMaxHeight is passed in a zero value, the implementation should be exactly the same as COpenFontFile::GetNearestFontToDesignHeightInPixelsL().

  4. As part of the ECOM framework, the resource file (.rss) is essential for your plug-in. This is example rss file for OFS plug-in.
<pre>#include "RegistryInfo.rh"
RESOURCE REGISTRY_INFO theInfo
{
  dll_uid = 0x20009F34;
  interfaces =
  {
    INTERFACE_INFO
    {
      interface_uid = 0x101F7F5D; //KUidOpenFontRasterizerPlunginInterface
      implementations =
      {
        IMPLEMENTATION_INFO
        {
          implementation_uid = 0x20009F34;
          version_no = 1;
          display_name = "FontRouter";
          default_data = "Font Enhancement Plugin";
          opaque_data = " ";
        }
      };
    }
  };
}</pre>

The &#8220;dll\_uid&#8221; should be replaced with the UID allocated by Symbian Signed, and &#8220;implementation\_uid&#8221; can the same as &#8220;dll_uid&#8221;.

  5. Directory difference.
<pre>Directory   pre-Symbian 9    Symbian 9
DLL file    /system/fonts    /sys/bin
RSC file    -                /resource/plugins
Font files  /system/fonts    /resource/fonts</pre>

RSC file is compiled from the resouce definition file (.rss).</ol>