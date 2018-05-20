---
id: 841
title: 在Google App Engine中使用泛域二级域名
date: 2010-01-30T18:40:39+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=841
permalink: /2010/01/30/use-wildcard-domains-in-google-appengine/
dsq_thread_id:
  - "250428344"
  - "250428344"
categories:
  - Development
tags:
  - appengine
  - Domain
  - google app engine
  - Java
  - wildcard
---
Google App Engine（以下简称GAE）除了支持自有的appspot.com域名外，借助Google Apps，它还允许用户配置自己的独立域名提供服务。但之前使用过独立域名的朋友可能都遇到过一个相同的困扰：你可以用指定一个特定的二级域名访问你的应用，但却无法使用泛域二级域名（wildcard sub-domain）。对泛域支持的[社区呼声](http://code.google.com/p/googleappengine/issues/detail?id=113)一直都很强烈，Google也声称将要支持这一特性，但却未给出具体的时间表。

前两天为了解决tb.ly的泛域二级域名，折腾了很久。因为虚拟主机服务商Dreamhost不对非Private Server用户支持DNS泛域解析，所以我不得不另谋它策。在GAE上的一次没头没脑的尝试，居然意外的让我发现GAE已悄然支持了泛域二级域名。配置过程稍微有些复杂，所以在这里完整整理出来，以tb.ly的真实案例，分享给各位研究GAE的朋友。

<!--more-->首先需要为你的域名（顶级或子域名均可，比如我的“tb.ly”）

[申请Google Apps服务](http://www.google.com/apps/)，这是在GAE中配置独立域名的前提。申请免费的Standard版本即可。

然后就可以在GAE管理面板中选择Administration / Application Settings / Domain Setup / Add domain&#8230;，填入你的域名（比如“tb.ly”）。按照向导一步一步完成配置（可参考[GAE的一篇教程](http://code.google.com/appengine/articles/domains.html)），最后你会被带到Google Apps的应用配置界面，这里及可以为你的应用添加二级域名了。点“Add new URL”，会出现一个输入二级域名的输入框。**Google并没有告诉你，其实这里只要输入“*”即可享受泛域二级域名了~**

完成上述配置后，试试在浏览器的地址栏输入任意一个二级域名（比如“oasis.tb.ly”），如果看到了你熟悉的应用界面，那么恭喜你，你已经成功完成了必要的配置！如果无法访问，也别灰心，很可能是由于你的DNS配置需要一些小小的调整。泛域域名需要在DNS配置中设定对应的泛域解析，具体而言，就是增加一条CNAME：*，指向ghs.l.google.com.（也可以是你自己为绑定ghs而创建的CNAME条目）。完成这项配置后，尝试ping一个任意二级域名，如果显示的回应主机名为ghs.l.google.com，就代表配置OK了。当然，如果回应主机没错，但ping的结果是timeout，那就涉及到另外一个复杂的国情问题，不在本文的讨论范畴内了。

至此为止，假设你已经成功的完成了上述步骤（还有任何我没有解释到的问题，欢迎留下评注或来信与我讨论）。那么下面我就拿tb.ly的例子演示一下如何在GAE的应用中识别和处理泛域二级域名：（我基本只用Java版，所以很抱歉不能同时覆盖Python的情形，不过相信这对熟悉GAE开发的朋友来说也不算是一个大问题）

<pre>package ly.tb;

import java.io.IOException;
import java.net.URL;
import java.util.Iterator;
import java.util.NoSuchElementException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.google.appengine.repackaged.com.google.common.base.Splitter;

public class SubDomainRedirector extends HttpServlet {

	@Override
	protected void doGet(final HttpServletRequest req, final HttpServletResponse resp) throws ServletException, IOException {
		final String host = new URL(req.getRequestURL().toString()).getHost();
		try {
			final String token = Splitter.on('.').split(host).iterator().next();
			if (token.equals("www"))
				resp.sendRedirect("http://tb.ly");
			else
				resp.sendRedirect("http://" + token + ".taobao.com/");
		} catch(final Exception e) {
			resp.sendRedirect("http://tb.ly");
		}
	}

	private static final long serialVersionUID = 1L;
}</pre>