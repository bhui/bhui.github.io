---
id: 1182
title: 对Android Wearable SDK的猜想
date: 2014-03-16T16:20:17+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=1182
permalink: /2014/03/16/prediction-for-the-upcoming-android-wearable-sdk/
categories:
  - Misc
---
【背景】

Android团队早在去年初启动开发的4.3版本，就已经开始为可穿戴设备优化Android OS及其SDK了。Bluetooth 4.0 LE (Smart)的支持是一个毋容置疑的信号；而NotificationListenerService从AccessibilityService中的脱离，可以看作是Android为在第三方设备的通知投射扫清了障碍。Android 4.4的瘦身和内存优化更是直指512M内存级别的低配置设备，已经为嵌入可穿戴设备铺平了道路；而传感器事件的硬件级批量聚合及新的计步传感器支持更是将Android的野心袒露无疑。其它诸如Immersive Mode和Translucent System UI（榨干受限的显示面积）、Enhanced notification access（更全面的通知信息及Actions交互的支持）、Storage Access Framework（集中存储和远程访问）等等新特性中都能找到可穿戴设备的端倪。

[在上周的SXSW上，Sundar Pichai宣称将会在2周内发布Android Wearable SDK](http://www.theverge.com/2014/3/9/5487750/google-to-help-developers-use-android-on-wearable-devices)，想必整个工程已经进入了最后的收官阶段。那么我不妨斗胆来预测一下几天后即将面试的Wearable SDK到底会长什么样。

【概貌】

Sundar Pichar在SXSW上也提到了他们认为的智能手机与可穿戴设备间的协同关系：『手机为中枢，穿戴皆IO』。（……smartphones became tiny computers, wearables are becoming nexuses of an array of sensors.）这说明Google不单单是希望把搭载了Android系统的可穿戴设备纳入生态，而要让『率土之滨，莫非王臣』。这也迎合了整个可穿戴生态的两条发展主线：提供富交互的完备设备 和 仅采集数据（及提供简单反馈）的哑设备。即便是未搭载Android系统的Pebble也好，Gear 2也罢，只要看作是手机的IO，就逃不出Android生态。

Google在可穿戴设备领域的处女作可谓是倾城的惊艳，但Google Glass很长时间以来只提供了非常受限的云端接入接口，让本就已经稀缺的开发人员抓狂不已，甚至于直接转向了root社区。好在Google最终在去年11月发布了Glass DevKit的早期预览版，开启了Glass本地App的大门。虽然Glass的交互迥异于目前常见的手腕类穿戴设备，但其SDK的设计思想则是非常明确而一致的，即基于目前Android SDK的更上层Addon SDK。考虑到离下一个Android大版本发布（Google I/O）至少还有3个月的这一时间点，相信这也将会是Wearable SDK第一版的基础形态。

SDK中可能会包含哪些有意思的设计呢？还是循着Sundar Pichar的线索顺藤摸瓜吧。『We want to develop a set of common protocols by which they can work together…… they need a mesh layer and they need a data layer by which they can all come together.』这里面传达了两个重要的信息：**互操作性协议、数据交换标准。前者让彼此间的IO更加顺畅互通，后者可助任何数据为任何App所用。**于是整个SDK的面目便可窥见一斑了。

【互操作性】

互操作性协议解决的典型场景便是Pebble这样的设备如何与Android App更方便的互通。Pebble SDK提供了一个私有的解决方案 —— Pebble端的Watch App（C语言开发）及其SDK提供的通信封装。这带来了一个Google最不希望面对的问题 —— 生态的分裂（Fragmentation）。因此，Wearable SDK需要以一个非常Android化的方式解决这个问题。除了已被广泛使用的『Notification Listener Service』外，我猜想中新的答案可能会是**『Widget』和『Remote Sensor』**。

『Widget』是从Android诞生早期就支持的唯一一个天然适合于可穿戴设备的前瞻设计，基于预定义受限面积的周期或事件驱动的渲染，然后将渲染好的位图传递给另一个负责展现widget的画布主体，后者可以接收简单的点击和手势交互，并将其反馈给提供widget的应用，触发新一轮的重绘。原先App与Launcher间的互操作性，在Android 4.2开始已经拓展到了锁屏界面（Lock Screen Widget），如今又可以无缝的过渡为App与穿戴设备间的桥梁。更重要的是，目前数不尽的带有Widget的App就可以摇身一变成为『可穿戴设备友好』的App了。Wearable SDK需要做的只是搭建起这样一个延伸性的透传协议。至于Android 4.2开始支持的『Secondary Display』多屏联动机制，也许不会出现在早期的Wearable SDK中，但有望成为未来面向具有大尺寸显示界面和高速无线连接能力（如Bluetooth 3.0 HS）的穿戴设备更灵活的媒体显示解决方案。

『Remote Sensor』，顾名思义，就是不在当前设备上的传感器。由于大量可穿戴传感单元的涌现，弥补了智能手机本身传感器的可触达边界，毕竟穿戴在身上的设备才能更准确的采集心跳、血压等生理指标，而各类借助现代传感技术的奇特探头才能满足人们日益多元化的对身周环境的感知需求。但持续传输的能耗问题是拦在Remote Sensor发展道路上的主要障碍，毕竟Android 4.4提供的Sensor Batch机制在降低耗电的同时是以牺牲实时响应能力为代价的。真正的救星是近几年方兴未艾的SensorHub技术，通过一个低功耗设计的可编程嵌入式芯片，先行采集和缓存传感器数据，并进行相对有限的实时分析，当预置条件满足时才激活主CPU进行处理。例如Moto X引以为傲的X8体系。再看可穿戴领域的传感器单元设计，只需将SensorHub前移至传感器单元内，单元与手机之间维持Bluetooth LE连接，SensorHub只在必要的时候通过这个连接通知手机和传输数据，而手机则可以在有需求时向传感器单元主动请求数据回传。得益于Android良好的传感器框架设计，以上Remote Sensor机制只需在现有Android框架下通过Sensor Agent over Bluetooth LE以虚拟传感器的形式提供，在上层App看来和手机本身的传感器并无二致。

【数据交换】

互操作性的分裂问题得到解决，并不意味着广大开发者就可以轻松的开发支持可穿戴传感器单元的App了。眼下的局面是，Kickstarter和Indiegogo上大量涌现的智能传感器众筹项目都是各自为阵，这些团队都不得不投入大量精力自己为其产品开发智能手机App，结果还往往不尽如人意；另一方面，传统App开发者似乎都只能隔山观火，既下不了场，也捞不到汤。这种维度的分裂正是由于移动OS平台上传感器数据规范化缺失和领域技术与应用层面间的断层所造成的。幸运的是，衔接开发者，正是Google在Android中所一贯擅长的。

Wearable SDK正应担起这付扁担，一方面定义更广泛和通用的原始传感器数据协议，另一方面提供高阶抽象的虚拟传感器框架，将这种基于数据整合和领域算法的抽象能力开放给社区和学术界，让更多拥有领域经验的专家和开发者进来衔接『专业数据』与『高阶应用』两个位面，培育出众多高质量的虚拟传感器。如此一来，才能让生态的两端更融洽的衔接，让更多的生活类和生产力App也能与可穿戴设备的蓬勃发展相互促进。

【结语】

YY了这么多，其实都是作为一个Android资深开发者兼可穿戴设备控的一些美好愿望。不过相信在汲取了Android发展历程中的坎坷之后，Google不会在这个新的领域让我们失望。就让整个社区一起迎接即将到来的Wearable SDK吧。

【题外话】

补充一个身为Geek的不切实际的畅想，Android Accessibility框架所蕴含的抽象展现和交互代理能力其实有非常大的潜力成为衔接传统App与可穿戴设备异化交互的玄铁重剑。但亟需提升Android整体体验的Google，想必是不会在Wearable SDK中祭出这件难以驾驭的武器了。好在Android生态的开放性并不阻碍Geek社区朝着这条道路挺进，也许在不久之后，我们就能看到一个可以在智能手表上操控手机端任意Android App的利器了。