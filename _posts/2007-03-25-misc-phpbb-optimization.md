---
id: 221
title: phpBB论坛优化拾零
date: 2007-03-25T17:56:15+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/2007/03/25/misc-phpbb-optimization/
permalink: /2007/03/25/misc-phpbb-optimization/
dsq_thread_id:
  - "250427429"
  - "250427429"
categories:
  - Internet
---
今天对[FontRouter论坛](http://fontrouter.oasisfeng.com/forum/)进行了少许的优化。当初为了图省事儿，直接用Dreamhost的One-click Install架设了一个基于phpBB的论坛，没想到后期维护起来竟然如此麻烦。

phpBB没有一个便于扩展的插件机制，所有的第三方优化都基于对代码的直接修改，美其名曰“MOD”。不用我在这里评论，自己动手安装过MOD的人恐怕都对其“易用性”深有体会吧。不过话说回来，MOD的优势在于性能和灵活度，不必浪费冗余的代码支撑繁复的插件stub，所以自然要快不少，这恐怕是Dreamhost在One-click Install中采用phpBB的最主要原因吧。从另一个角度来讲，通过MOD的安装和调整，我倒是在PHP语言的学习上进步了不少。 🙂

今天主要进行了一些本地化调整和SEO工作：

**（1）调整了subSilver模板的CSS，将所有11点阵以下的字体全部提升至11点阵，这是中文字体显示的底线。**只因我一直使用Firefox（设置了强制最小字体），所以时至今日才发现这个重要的本地化视觉缺陷。

**（2）将subSilver模板中默认的内嵌CSS替换为外部.css文件引用（修改template/subSilver/overall_header.tpl文件）。**这个其实说不上是优化，因为我一直没有注意到subSilver模板的这个默认行为，导致每页的带宽消耗白白浪费了10k余……

**（3）修改了页面TITLE的生成规则，去掉了冗余了文字，加入了站点描述：**
  
首先是修改template/subSilver/overall_header.tpl文件，将原有的<title>&#8230;</title>替换为：

<title>{PAGE\_TITLE} :: {SITENAME} &#8211; {SITE\_DESCRIPTION}</title>

然后分别修改view\_topic.php、view\_forum.php，去掉“$page_title=”后面的冗余部分，只保留主题/论坛名。

虽然只是一个小小的调整，不过其SEO效果却是不容忽视的，特别体现在AdSense的内容相关性实实在在提升了不少。 (:

**（4）调整了Google AdSense的布局**。撤掉了原来页面顶端和底端的两个横幅广告（事实证明，这种放置不恰当的BannerAd完全不会带来任何Click），代之以Post顶楼右侧的小幅广告。希望这个调整能为疲软的AdSense带来一点改观。（此前的点击率一直停留在10<sup>-5</sup>这个数量级上，差不多快对AdSense绝望了…… X-( ）

**（5）安装了phpBB Google Sitemap Generator v1.0.1**。这个MOD可以为你生成一个体面的Google Sitemap，不过Google Webmaster工具报告却提示其生成的Sitemap有语法错误。XML Validator检查了一下，发现它在<sitemap>下使用了<changefreq>，这是0.84的标准语法所不支持的，修改代码去掉之后就OK了。