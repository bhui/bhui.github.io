---
id: 292
title: Find the UIDs and Capabilities of Symbian EXE/DLL
date: 2007-12-14T09:26:11+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/12/14/find-uids-and-capabilities-of-symbian-executive/
permalink: /2007/12/14/find-uids-and-capabilities-of-symbian-executive/
dsq_thread_id:
  - "250427612"
  - "250427612"
categories:
  - Development
  - English
  - Symbian
tags:
  - Capability
  - DLL
  - EXE
  - Platform Security
  - Symbian
  - UID
---
### (1) Emulator Build (Win32 PE)

First, find the start address of section &#8220;.SYMBIAN&#8221; by typically using &#8220;dumpbin /section:.SYMBIAN <Excutable File>&#8221;.

The output looks like:

<pre>SECTION HEADER #6
.SYMBIAN name
30 virtual size
17000 virtual address (00417000 to 0041702F)
1000 size of raw data
17000 file pointer to raw data (00017000 to 00017FFF)
0 file pointer to relocation table
0 file pointer to line numbers
0 number of relocations
0 number of line numbers
C0000040 flags
Initialized Data
Read Write</pre>

According to the line containing &#8220;virtual address&#8221;, section &#8220;.SYMBIAN&#8221; starts at address 0x00017000.

Now, use any hex-editor to view the content at this address:

> 00017000h: 7A 00 00 10 00 00 00 00 B2 97 1F 10 5E 01 00 00
  
> 00017010h: B2 97 1F 10 57 B6 1F 10 **B6 E1 0F 00** 00 00 00 00

The first 3 dwords are UIDs: 0x1000007A stands for &#8220;Symbian EXE&#8221;, 0x101F97B2 is the unique UID of this file. (no UID2 for Symbian EXE, but this field is essential for DLL to indicate the framework, eg. 0x10009D8D for ECOM)

The capabilities field at offset 0x18h holds all the capabilities for this executive in the form of bitmask. Thus, 0x000FE1B6 is translated to the following capabilities: (see enumerator TCapability in Symbian SDK)

CommDD PowerMgmt ReadDeviceData WriteDeviceData TrustedUI ProtServ NetworkServices LocalServices ReadUserData WriteUserData Location SurroundingsDD UserEnvironment

### (2) Target Build (Symbian PE)

3 UIDs located at the very beginning of the executive file, and the capabilities field is at fixed offset 0x88h. (same meaning as described for emulator build)