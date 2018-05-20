---
id: 264
title: How to use font in Symbian
date: 2007-08-20T23:05:03+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/08/20/how-to-use-font-in-symbian/
permalink: /2007/08/20/how-to-use-font-in-symbian/
dsq_thread_id:
  - "250427484"
  - "250427484"
categories:
  - Development
  - English
  - Symbian
tags:
  - baseline
  - Font
  - Swiss
  - Symbian
  - wiki
---
## 1. Forget about the stupid &#8220;Swiss&#8221;.

As you may have already read the section &#8220;How to select a font&#8221; in Symbian SDK documents, the follow example code snippet show us the way of selecting a font.

<pre><span class="code-comment">// Get an alternative font
</span>_LIT(KMyFontName,<span class="code-quote">"Swiss"</span>);
CFont* myFont;
TFontSpec myFontSpec(KMyFontName,1); <span class="code-comment">// to get smallest Swiss font
</span>CGraphicsDevice* screenDevice=iCoeEnv-&gt;ScreenDevice();
screenDevice-&gt;GetNearestFontInTwips(myFont,myFontSpec);
...</pre>

Before getting closer to the font mechanism and typeface design of Symbian, some guys have tried the code in their application and things work well. That&#8217;s why I saw this typeface name &#8220;Swiss&#8221; appear even in many commercial applications. In fact, there is no typeface named &#8220;Swiss&#8221; built-in with S60 phones, so what you get from the code above is the most closely approximate font, but may not the font really suitable. For instance, &#8220;Swiss&#8221; will make your application not compatible with East-Asian phones. To grab a better view of &#8220;How to select a font&#8221;, just read on.
  
<!--more-->

## 2. In common applications, try not to use custom fonts, but use predefined or logical fonts.

**No fonts should be assumed existent in user&#8217;s phone** because the actual typeface names usually vary with UI classes, and even with phone languages. For example, English S60 v1 phone has primary fonts: LatinBold12, LatinBold13, LatinBold17, LatinBold19 and LatinPlain12, but the Chinese model only has CombinedChinesePlain12 and CombinedChinesePlain16 as its primary fonts. If you directly use &#8220;LatinBold12&#8221; in your application, it will result in Chinese characters missing for text input and display. If you take a look at UIQ phones, the typeface names are also totally different.

For maximum compatibility and flexibility, you may use predefined fonts which are preadapted to actual existing fonts in any Symbian phones. There are 6 predefined fonts for common use in class **CEikonEnv**: **NormalFont()** (inherited from class **CCoeEnv**), **AnnotationFont()**, **TitleFont()**, **LegendFont()**, **SymbolFont()**, **DenseFont()**. If you think the predefined fonts are ambiguous and want to specify the basic attributes, **CEikonEnv::Font(const TLogicalFont& aLogicalFont)** gives you the chance. By specifying the category and style, you will get the most suitable font.

## 3. Never assume that the specification of font obtained is the same as requested.

As mentioned above, no fonts should be assumed existent in client environment. Even if you request the font with the typeface built-in, you may not get the expected one. <ins>[1]</ins> Therefore do not layout your application UI exactly with the prechosen font specifications. Make allowance for discrepancy of actual font obtained and use the measuring APIs to format paragraphs and long lines.

**TextUtils::ClipToFit()** is a good choice for truncating long text according to the font specification, and **CFont::TextWidthInPixels()** measures the given text with the font specified. <ins>[2]</ins>

## 4. Not all fonts have descent.

<p class="codeContent">
  Some East-Asian fonts have zero descent, because their character structure and style is not the same as Latin fonts. If the application you develop is for international users, please keep this in mind. Before using <strong>CGraphicsContext::DrawText()</strong> with parameter <strong>aBaselineOffset</strong>, calculate it with the following formula:
</p>

<pre>Baseline Offset = (Line Height + Font Ascent - Font Descent) / 2 [3]</pre>

Font ascent and descent are directly retrieved from class **CFont**, and line height is the height of available space for Text drawing.

On the other side, some Chinese application developers erroneously assume that all fonts have no descent and thus lead to text sinking or underflow when their applications run in non-Chinese phones.

## 5. For font-customizable applications, make sure all the font attributes are available to users.

In font-customizable applications, such as text viewer, user may customize the font for personal preferences. As a partial example, <span class="nobr"><a href="http://www.qreader.com/" title="Visit page outside Confluence" rel="nofollow">QReader</a></span> provided some customizable attributes in its &#8220;Settings &#8211; Font&#8221; dialog. To enumerate all available fonts in the phone, use **NumTypefaces()** and **TypefaceSupport()** of class **CWsScreenDevice**(inherited from **CGraphicsDevice**) to walk through all typefaces. Besides typeface name and height, other customizable attributes of fonts are: Posture, Stroke Weight, Mono-width and Render Style. The Render Style is also called bitmap type in Symbian SDK, and it is a version related attributes. Symbian 6 does not support bitmap type while Symbian 7 and later started to support anti-aliased bitmap type. In the newer Symbian 9.2, Sub-pixel bitmap type is added, but actually there is no font rasterizer which supports sub-pixel bitmap type yet.

More text style is available in addition to font attributes. Underline and Strike-through effects are applied through class **CGraphicsContext** as they are text styles but not font attributes.

> [1] Some third-party software enhances the management of font in Symbian, such as <span class="nobr"><a href="http://fontrouter.oasisfeng.com/" title="Visit page outside Confluence" rel="nofollow">FontRouter</a></span> which replace the built-in fonts with user preferred ones and provide more adjustment on font specification.
> 
> [2] Paragraph and UI elements formatting are UI class related. If your application is built on S60, please refer to class **AknTextUtils** for more details.
> 
> [3] Some of the example code in Symbian SDK used incorrect formula to calculate baseline offset that may lead to text sinking or underflow.

[This article is posted on Symbian Develop Network Wiki.](http://developer.symbian.com/wiki/display/papers/How+to+use+font+in+Symbian)