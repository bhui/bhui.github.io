---
id: 1095
title: 阿里云主机试用体验
date: 2012-08-13T20:16:26+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=1095
permalink: /2012/08/13/experience-the-aliyun-cloud-hosting/
categories:
  - Internet
tags:
  - Aliyun
  - VPS
  - 云主机
  - 盛大云
  - 阿里云
---
内部受邀试用了一下[阿里云主机](http://www.aliyun.com/product/vm)，让我此前对阿里云的印象有所改观。在云主机产品上，感觉阿里云还是比较能沉下心来客观面对国内的中低端市场的，并没有摆出阳春白雪的姿态来。

尽管内部试用邀请是针对『标准A型』的规格，但我坚持换成了『经济A型』，因为最低端的型号往往更能看出一家主机公司的态度和良心。

**规格**

阿里云主机目前的规格搭配，感觉不是特别合理，可能影响到成本及性价比。比如经济A型，单核、512M内存，60G空间，1Mbps的带宽。在这个CPU及内存规格下，空间显得太充裕，而带宽则较局促。相比之下，盛大的云主机似乎更为人性化，类似的规格『超微』，也是512M内存，存储是7.5G，带宽可独立选配（这一点是大爱），更贴合小型创业团队的需求。（也许阿里云更多面向的是电商建站，规格需求略有不同）

从阿里云的产品线布局来看，存储方案应会主推OSS和RDS。或许限制主机带宽是推广OSS的一个市场策略，但大容量的主机存储却感觉与这个目的背道而驰。

**价格**

因为阿里云主机的规格是绑定了带宽的，所以跟盛大云对比，同规格的价格差不多各有胜场。但是考虑到盛大云的规格搭配对小型互联网初创产品更为合理，而且带宽规格可以分开购买，就显得更有性价比了。

<p style="padding-left: 30px;">
  <strong>注：<a href="http://www.aliyun.com/cps/promotion_check?promotion_code=uUddqfuxAdDu8NSMV7vzyAg5Yt4OgcczFlfA5S6zk0wEfvC%2FXWmbrqGdDPEqO4i3rgFm%2FA2Ho45ixbuZW6zX0MqZZVpKktWBVaJjkl%2BrRAgGsiBio9NFvnM1%2Bf5FRl6ERLyvYQYqUzYLTTW9uMAD83lXApkAg3Y9">最近阿里云的高调团购促销</a>，让价格无形中增添了相当的吸引力。预付一年省两个月，实际享受最高16个月（视团购成交量），还可以<a href="http://www.aliyun.com/topic/sanjianke/">升级到1G内存和2Mbps带宽</a>（对应『经济A型』）。相当于￥66/月的价钱购买接近『经济B型』的规格，已经比大多数国内VPS服务商的促销给力很多了。</strong>
</p>

**配置**

基于Xen PV虚拟化技术，目前提供的OS安装选项有点少，尤其是32bit系统，只有CentOS 5.3一个选择，对于选择小规格主机的用户有些不便。毕竟小规格主机，尤其是在内存有限的情况下，更倾向于使用32bit系统以节省内存。

后台因为上线不久的缘故，还显得略微粗糙了些，小问题不少，不过都影响不大，但其中有一点需要特别小心：管理控制太上面的停止和重启操作，是没有任何确认过程的。这样一个下拉选择框执行关键的维护动作，稍有不慎就误操作了……

**性能（测试篇）**

用hosting社区标准的性能测试工具unix-bench作了一个简单的横向测试（测试条件有限，数据仅供参考）。作为对比的几款主机除了大家所熟知的Linode 512之外，还有Lightwave的Xen VPS，阿里云的老双开集群Linux主机。

<table border="1" cellspacing="1" cellpadding="1" align="left">
  <tr>
    <th scope="col">
    </th>
    
    <th scope="col">
      Aliyun Eco.A
    </th>
    
    <th scope="col">
      Lightwave PV.Tiny
    </th>
    
    <th scope="col">
      Linode 512
    </th>
    
    <th scope="col">
      Aliyun Old
    </th>
  </tr>
  
  <tr>
    <td>
      Specifications
    </td>
    
    <td>
      Virt 1 core
    </td>
    
    <td>
      Virt 8 cores
    </td>
    
    <td>
      Virt 4 cores
    </td>
    
    <td>
      Virt 2 cores
    </td>
  </tr>
  
  <tr>
    <td>
      Dhrystone 2 using register variables
    </td>
    
    <td>
      2127.5
    </td>
    
    <td>
      1929.0
    </td>
    
    <td>
      <strong>3024.8</strong>
    </td>
    
    <td>
      2170.6
    </td>
  </tr>
  
  <tr>
    <td>
      Double-Precision Whetstone
    </td>
    
    <td>
      523.7
    </td>
    
    <td>
      <strong>2572.6</strong>
    </td>
    
    <td>
      1375.3
    </td>
    
    <td>
      925.6
    </td>
  </tr>
  
  <tr>
    <td>
      Execl Throughput
    </td>
    
    <td>
      836.0
    </td>
    
    <td>
      596.7
    </td>
    
    <td>
      564.0
    </td>
    
    <td>
      <strong>1673.0</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      File Copy 1024 bufsize 2000 maxblocks
    </td>
    
    <td>
      <strong>2190.0</strong>
    </td>
    
    <td>
      556.3
    </td>
    
    <td>
      783.7
    </td>
    
    <td>
      280.1
    </td>
  </tr>
  
  <tr>
    <td>
      File Copy 256 bufsize 500 maxblocks
    </td>
    
    <td>
      <strong>1495.3</strong>
    </td>
    
    <td>
      441.2
    </td>
    
    <td>
      489.7
    </td>
    
    <td>
      183.4
    </td>
  </tr>
  
  <tr>
    <td>
      File Copy 4096 bufsize 8000 maxblocks
    </td>
    
    <td>
      <strong>2939.5</strong>
    </td>
    
    <td>
      826.4
    </td>
    
    <td>
      1573.5
    </td>
    
    <td>
      461.2
    </td>
  </tr>
  
  <tr>
    <td>
      Pipe Throughput
    </td>
    
    <td>
      1436.6
    </td>
    
    <td>
      <strong>1985.2</strong>
    </td>
    
    <td>
      1242.4
    </td>
    
    <td>
      1527.8
    </td>
  </tr>
  
  <tr>
    <td>
      Pipe-based Context Switching
    </td>
    
    <td>
      776.4
    </td>
    
    <td>
      716.8
    </td>
    
    <td>
      440.3
    </td>
    
    <td>
      <strong>1429.7</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      Process Creation
    </td>
    
    <td>
      966.8
    </td>
    
    <td>
      532.4
    </td>
    
    <td>
      407.8
    </td>
    
    <td>
      <strong>1822.5</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      Shell Scripts (1 concurrent)
    </td>
    
    <td>
      1036.6
    </td>
    
    <td>
      1471.0
    </td>
    
    <td>
      1355.7
    </td>
    
    <td>
      <strong>2396.1</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      Shell Scripts (8 concurrent)
    </td>
    
    <td>
      989.5
    </td>
    
    <td>
      1347.6
    </td>
    
    <td>
      1275.7
    </td>
    
    <td>
      <strong>2516.0</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      System Call Overhead
    </td>
    
    <td>
      2147.2
    </td>
    
    <td>
      1049.8
    </td>
    
    <td>
      <strong>838.5</strong>
    </td>
    
    <td>
      895.1
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>System Benchmarks Index Score</strong>
    </td>
    
    <td>
      <strong>1290.3</strong>
    </td>
    
    <td>
      995.4
    </td>
    
    <td>
      937.0
    </td>
    
    <td>
      1045.8
    </td>
  </tr>
</table>

可以看出，阿里云主机的优势在于相当强劲的IO性能（可能受益于现阶段母机整体IO负载较低），而在整数运算方面，Linode的优势更为明显；Lightwave的浮点性能强劲得益于它的AMD Opteron CPU。遗憾的是，在系统调用的开销上，阿里云主机似乎显得不太正常的高，可能与采用的虚拟机架构及参数调优有关。整体得分，仍然是阿里云主机胜出，显示出了阿里云主机目前在规格方面相当的诚意。

对于大部分Web或Mobile应用来说，主要关注整数和IO性能两方面，其次关注系统调用开销。JVM型后端可以不用太过关注进程创建和pipe方面的性能。

**性能（感受篇）**

为了有一个更为直观的感受，我在阿里云的主机上测试了一下Android源码的编译（CyanogenMod 10），首次编译大约耗时8小时，增量编译在2小时多一点。整体来说感觉比较满意。

操作过程中，shell的整体响应很稳定，没有出现国外低端VPS常见的卡顿（非网络原因）。

网络性能由于暂时没条件作国内云主机间的对比测试，就简单说一下直观感受吧。测试100M单线程下载，下行速度稳定在标称的带宽限额上，而上行带宽则没有作带宽限制，测试过程中曾经稳定达到了8M/s，这一点非常适合上行带宽需求不小的应用类型。

**总结**

整体上，阿里云主机给人的感觉是中规中矩，仍有较多值得改善的方面。但在一些细处，仍显示出特殊的吸引力，例如强悍的IO性能、无限制的上行带宽、高质量的双线阿里机房。作为一家国内一线的主机服务商，售后服务和技术实力方面还是有所保障的。鉴于阿里云敢于作出[『100倍故障时长赔偿』的承诺](http://www.aliyun.com/topic/fuwutixi/)，看来对于自己的可靠性技术相当自信。

无论是国内的小规模初创团队，还是Geek们希望跨越电信/联通的互通鸿沟，都值得趁阿里云此次[难得力度的促销优惠](http://www.aliyun.com/cps/promotion_check?promotion_code=uUddqfuxAdDu8NSMV7vzyAg5Yt4OgcczFlfA5S6zk0wEfvC%2FXWmbrqGdDPEqO4i3rgFm%2FA2Ho45ixbuZW6zX0MqZZVpKktWBVaJjkl%2BrRAgGsiBio9NFvnM1%2Bf5FRl6ERLyvYQYqUzYLTTW9uMAD83lXApkAg3Y9)，低价入手这个还处在培育期的云主机，至少可以少受小型主机服务商普遍的超售困扰。