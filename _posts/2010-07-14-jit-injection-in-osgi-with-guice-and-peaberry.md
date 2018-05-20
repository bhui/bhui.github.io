---
id: 882
title: 用Guice+Peaberry实现OSGi环境下的JIT注入
date: 2010-07-14T00:53:03+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=882
permalink: /2010/07/14/jit-injection-in-osgi-with-guice-and-peaberry/
dsq_thread_id:
  - "255182922"
  - "255182922"
categories:
  - Development
tags:
  - DI
  - Guice
  - JIT
  - OSGi
  - Peaberry
---
Guice是一个Java下非常强大的依赖注入框架，相比其它同类框架，我更喜欢Guice这种“配置亦代码”的风格。除了开发友好性之外，Guice的过人之处还体现在它灵活的JIT(Just-in-time)注入上。利用@ProvidedBy()注解可以方便的为接口绑定定制的Provider，从而实现结合了动态逻辑的Lazy注入。

当Guice和OSGi框架碰撞到一起时，就会遇到一些观念上的矛盾：OSGi的动态生命周期在Guice本身的静态绑定下无法发挥其应有的作用，而Dynamic Service也无法方便的与Guice对接。好在开源社区已经有人意识到这些问题，并为两者搭起了一座鹊桥，这个项目就是“[Peaberry](http://peaberry.googlecode.com/)”。

这两天在捣腾Peaberry时，发现它的设计主要是针对静态绑定，在与Guice的JIT注入一起用时，却还差那么一两块砖，于是自己把它给砌上了，顺便分享出来与大家交流一下。

按照Peaberry的用户手册，静态绑定一个DS服务的写法是在Module.configure()中使用：（以LogService接口为例）

<pre lang="java5">bind(LogService.class).toProvider(Peaberry.service(LogService.class).single());
</pre>

如果转为JIT注入，则必须提供一个相应的Provider类。虽然Peaberry.service(&#8230;).single()返回的正是一个Provider，但鉴于Java注解只能用字面类（Literal Class），所以这里需要包装一下。我的办法是定义一个抽象的公共Provider，用反射去识别派生类的具体泛型类型：

<pre lang="java5">public abstract class JitProvider&lt;T> implements Provider&lt;T> {

	protected JitProvider() {
		@SuppressWarnings("unchecked")
		final Class&lt;T> clazz = (Class&lt;T>) ((ParameterizedType) getClass().getGenericSuperclass()).getActualTypeArguments()[0];
		provider = Peaberry.service(clazz).single().direct();
	}

	@Override
	public T get() {
		return provider.get();
	}

	@Inject
	protected void setInjector(final Injector injector) {
		injector.injectMembers(provider);
	}

	private final Provider&lt;T> provider;
}
</pre>

具体使用JitProvider的接口以如下形式声明：

<pre lang="java5">@ProvidedBy(Foo.Provider.class)
public interface Foo {
	...
	static class Provider extends JitProvider&lt;Foo> {}
}
</pre>

这样，所有使用Foo服务的Bundle都完全实现了即需即用，不必再像过去那样在每一个用到该服务的Bundle的Activator中事先进行一遍Peaberry繁琐的bind配置。经此精简优化，Peaberry的易用性得到了明显的提升，使用起来也更加直觉化了。