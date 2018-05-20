---
id: 316
title: 在Linux中实现虚桩式内核模块
date: 2008-06-28T20:38:46+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=316
permalink: /2008/06/28/linux-stub-kernel-module/
dsq_thread_id:
  - "250427796"
  - "250427796"
categories:
  - Linux
tags:
  - Kernel
  - ko
  - Linux
  - modprobe
  - Module
---
最近在把以前做的一个驱动程序在线加载技术移植到SuSE的AutoYaST安装系统中时遇到了一点小麻烦。AutoYaST采用SuSE自己编写的Linuxrc作为其初期引导部分，有别于大部分常规的initrd引导部分，Linuxrc是直接用C语言编写的，而且几乎没有提供什么扩充的灵活性。如此一来，就无法像以往移植到其它环境中那样单纯修改引导脚本就可以搞定。虽说直接修改Linuxrc的源码也可以达到这个目的，但这样就增加了后期维护的复杂度。唉，还真是个头疼的问题……

仔细分析了一下AutoYaST的设计，发现它至少还是允许增补驱动程序的，但仅仅支持最简单的用配置文件写死的insmod方式…… 好吧，只要还给了这个勉强算得上可扩充的途径，我一样能把驱动在线加载模块集成进来。由于只能固定调用某个驱动，所以必须从内核模块下手。把现有程序改造成内核模块显然是不现实的，好在Linux内核中还提供了这样一个调用用户态程序的接口：call_usermodehelper()，你可以在kmod.h中找到它。功能很简单，调用一个用户态程序，并且可以选择是否阻塞直到它执行完成。

<!--more-->顺着这个思路，只要写一个简单的虚桩式内核模块，在其初始化函数中调用我们真正想要执行的用户态程序即可达到目的了。但是，当我提出这个方案后，立即有同事质疑：在内核模块初始化阶段加载别的内核模块，搞不好会锁死内核吧？“搞不好”至少说明他也不肯定，为了找寻答案，我分析了一下内核中系统调用sys\_init\_module()的代码（以2.6.17为蓝本）。

<pre>asmlinkage long
sys_init_module(void __user *umod,
		unsigned long len,
		const char __user *uargs)
{
	......

	/* Only one module load at a time, please */
	if (mutex_lock_interruptible(&module_mutex) != 0)
		return -EINTR;</pre>

刚进入就加锁了，似乎有点不妙。紧接着开始加载内核模块：

<pre>/* Do all the hard work */
	mod = load_module(umod, len, uargs);
	if (IS_ERR(mod)) {
		mutex_unlock(&module_mutex);
		return PTR_ERR(mod);
	}

	/* Now sew it into the lists.  They won't access us, since
           strong_try_module_get() will fail. */
	stop_machine_run(__link_module, mod, NR_CPUS);

	/* Drop lock so they can recurse */
	mutex_unlock(&module_mutex);

	blocking_notifier_call_chain(&module_notify_list,
			MODULE_STATE_COMING, mod);

	/* Start the module */
	if (mod->init != NULL)
		ret = mod->init();</pre>

看来这段代码的作者（或维护者）似乎早就预见到了我所面临的场景。内核模块的加载和初始化被清晰的分为两步，由于加载过程需要链接内核模块，因此必须加锁，而后续的初始化过程已经不会影响内核的完整性了，所以自然可以在解锁后进行。

排除这个疑虑后，我写了一个简单的用于检验上述思路的内核模块：

<pre>#include &lt;linux/kernel.h&gt;
#include &lt;linux/module.h&gt;
#include &lt;linux/kmod.h&gt;

static int __init kmod_init(void)
{
        int ret;
        char *envp[] = {
                "PATH=/sbin:/bin",
                NULL
        };
        char *argv[] = {
                "/sbin/modprobe",
                "--first-time",
                "e1000",
                NULL
        };
        if ((ret = call_usermodehelper(argv[0], argv, envp, 1)) != 0)
                printk(KERN_ERR "Kmod test failed! (%d)n", ret);

        return ret > 0 ? - ret : ret;
}

static void __exit kmod_exit(void)
{
}

module_init(kmod_init);
module_exit(kmod_exit);

MODULE_LICENSE("GPL");</pre>

用insmod插入它时实际上调用了用户态的modprobe插入另一个内核模块e1000。如果不希望将这个虚桩留在内核中，也可以通过在kmod_init中返回-1将自身从内核中移除。

验证结果表明这个虚桩式内核模块的方案完全是可行的，而且与被加载的实际内核模块之间没有任何耦合及影响，它们可以各自独立的被卸载。