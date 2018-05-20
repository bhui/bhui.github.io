---
id: 307
title: Linux下可以替换运行中的程序么？
date: 2008-04-14T20:08:33+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=307
permalink: /2008/04/14/replace-running-program-in-linux/
dsq_thread_id:
  - "260925439"
  - "260925439"
categories:
  - Linux
tags:
  - cp
  - Demand-Paging
  - Linux
  - Shared Object
---
今天被朋友问及“Linux下可以替换运行中的程序么？”，以前依稀记得Linux下是可以的（而Windows就不让），于是随口答道“OK”。结果朋友发来一个执行结果：（test正在运行中）

<pre># cp test2 test
cp: cannot create regular file `test': Text file busy</pre>

看起来是程序被占用，无法覆盖。于是自己又再做了几个实验：

（1）先rm删除正在运行的test，然后cp test2 test就没有错误了。
  
（2）先mv改名正在运行的test，然后cp test2 test也没有问题。

<!--more-->查了查资料并动手分析了一下，找到了比较满意的解释。cp并不改变目标文件的inode，事实上它的实现是这样的：

<pre># strace cp test2 test  2&gt;&1 | grep open.*test
open("test2", O_RDONLY|O_LARGEFILE)     = 3
open("test", O_WRONLY|O_TRUNC|O_LARGEFILE) = 4</pre>

我原以为cp的实现是“rm + open(O_CREAT)”，不过现在想想上面的实现方式才是最可靠的（保证了时序安全和目标文件的属性）。这也可以解释为什么cp的目标文件会继承被覆盖文件的属性而非源文件。

Linux由于Demand Paging机制的关系，必须确保正在运行中的程序镜像（注意，并非文件本身）不被意外修改，因此内核在启动程序后会锁定这个程序镜像的inode。这就是为什么cp在用“O\_WRONLY|O\_TRUNC”模式open目标文件时会失败。而先rm再cp的话，新文件的inode其实已经改变了，原inode并没有被真正删除，直到内核释放对它的引用。同理，mv只是改变了文件名，其inode不变，新文件使用了新的inode。

问题到这里已经水落石出，不过刨根究底的个性驱使我再做了以下一组实验，没想到结果完全出乎我意料之外！

写了一个简单的测试程序：

<pre>#include &lt;stdio.h&gt;

int main(int argc, char * argv[])
{
    foo();  // An export function by libtest.so.
    sleep(1000);
    return 0;
}</pre>

foo()是另一个测试动态库libtest.so的导出接口，只打印一行提示就返回。接下来我把上面对执行文件的测试用例对动态库又做了一遍：

（1）cp libtest2.so libtest.so可以直接覆盖已加载的动态库。
  
（2）先rm删除已加载的libtest.so，然后cp libtest2.so libtest.so成功。
  
（3）先mv改名已加载的libtest.so，然后cp libtest2.so libtest.so成功。

除了第一个用例外，结果相同。这样看来，动态库被加载时难道ld并没有锁定inode？不过想想也可以宽恕，毕竟ld也是用户态程序，没有权利去锁定inode，也不应与内核的文件系统底层实现耦合。

到这里都还算在情理之中，看起来Linux也都处理的很好。不过还剩下一个问题：动态库被以cp的方式覆盖后难道不会和Demand Paging机制产生冲突？

在思考这个问题的过程中，我意识到前面这个测试程序的一个致命漏洞，稍作修改如下：

<pre>#include &lt;stdio.h&gt;

int main(int argc, char * argv[])
{
loop:
    foo();  // An export function by libtest.so.
    sleep(1);
    goto loop;
    return 0;
}</pre>

这次，再执行上面的三个用例后发现，“cp libtest2.so libtest.so”虽然仍可直接覆盖已加载的动态库，但是测试程序马上出现了“Segmentation fault”。而后两个用例结果不变。由此可见，想要安全的替换已加载的动态库，还是用“笨拙”的“rm + cp”吧，看似捷径的“cp覆盖”会直接葬送掉你的程序……

看来，我再一次低估了Linux的健壮性，看似符合逻辑的流程也可能会带来灾难性的后果；“rm & cp”与“cp覆盖”背后所隐藏的底层差异却可以成为你的救星。Linux用得越久越是让人觉得这是一块充满了荆棘和陷阱的原始丛林，只有步步为营实踏前行才能走的更远。

注：以上实验基于SuSE Linux Enterprise Server 9 SP1（Linux 2.6.5 & glibc 2.3.3）。