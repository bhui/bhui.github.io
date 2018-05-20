---
id: 1117
title: 基于Fragment的Android前台服务框架
date: 2012-10-02T22:39:48+00:00
author: oasisfeng
layout: post
guid: http://blog.oasisfeng.com/?p=1117
permalink: /2012/10/02/android-service-framework-based-on-fragment/
categories:
  - Development
tags:
  - Android
  - Fragment
  - Loader
  - service
---
从Android 3.0开始，Google引入了全新的Fragment UI体系，重新诠释了可复用可延展的Android UI设计理念。Android Support Library更是为任何面向低版本Android的应用开发者提供了完整的Fragment后向兼容方案（backport）。所以，如果开发一款新的Android应用，使用Fragment已无需有任何顾忌。尽早拥抱这一强大的机制设计，可以帮你省下可观的开发和维护工作量。

说起Service框架，大家可能已经比较熟悉，但将其与Fragment联系在一起，就多少有些让人觉得诧异了。我们不妨先来看看Android现有的标准Service框架，一般也称之为后台服务。官方文档中的定义是：一个可在后台执行长时间操作，不提供UI的应用组件。Service的主要特点是生命周期与应用的UI独立，不随应用退出而结束。后台服务的典型用途主要有两大类：执行不随应用切换而打断的任务（如下载、播放）或监听和响应系统事件（如来电、位置）。但在实际开发中，Service的实现复杂度并不低，一方面需要考虑并处理服务的生命周期，另一方面还要痛苦的处理服务与UI间的通信，倘若需要在服务代码中与用户交互，要么使用相当受限的Toast和Notification机制，要么实现一个复杂的UI回调……

实际上，在大部分的应用场景中，很多与UI相关的处理（即MVC中的Controller）也有类似后台服务一样的跨界面复用和共享需求，它们同时也与UI有着密切的联系，而且仅在应用打开时发挥作用，例如账户的全局状态、未读的通知消息、购物车等。这种需求我们一般称之为前台服务（Foreground Service）。过去，一部分的这种需求往往采用SharedPreference的方式在不同的界面间实现共享，这样做不仅有一些额外的开销（文件IO），同时数据类型和逻辑的受限也比较明显。而且，当状态较为复杂时，每次在状态切换（如屏幕旋转）后重建状态的性能代价也可能影响到用户体验。

其实，Fragment机制完全可以优雅的达成上述前台服务的需求，得益于Fragment本身与界面的紧密联系，可以方便的实现服务与UI的双向互通；受益于Fragment自动的生命周期管理，不必刻意提防内存泄露；借助Fragment的切换保留（retain）机制，可以在状态切换期间保持服务不中止。另外，由于Fragment的生命周期管理是由框架自动完成的，所以开发者也完全不必在Activity的生命周期事件代码中加入各种服务相关的冗赘处理，让代码更简洁清晰。**唯一的限制是，Fragment不能跨Activity共享。**不过按照基于Fragment的界面设计思想，相关联的UI组件都应基于Fragment实现，并置于一个共同的Activity之下，只有在生命周期可独立存在和延续的界面中才需要使用单独的Activity。因此，在严格按照Fragment设计思想开发的App中，这一限制并不是一个真正的问题。

如果你对Fragment的这种『特别用途』仍然持保留意见的话，不妨看看官方文档中的这一段表述：[『Adding a fragment without UI』](http://developer.android.com/guide/components/fragments.html#AddingWithoutUI)，它明确的暗示了这种使用方式的合理性与可行性。

接下来，就让我们一起来探索一个可行的基于Fragment的前台服务框架吧。

### （1）前台服务的创建、销毁和获取

与后台服务类似，前台服务通常也是『按需创建』的，因此服务的创建和获取可以封装在一个操作中。由于无UI的Fragment不能通过界面嵌入点的资源ID来访问，因此tag通常是唯一可靠的辨识和访问方式。（以下代码省略了部分异常处理）

<pre>private static final String KServiceTagPrefix = "service:";

public static &lt;T&gt; T getService(Class service_class, FragmentManager fm) {
  final String service_name = KServiceTagPrefix + service_class.getCanonicalName();
  @SuppressWarnings("unchecked") T service = (T) fm.findFragmentByTag(service_name);
  if (service == null) {
    Log.i(TAG, "Starting service: " + service_class.getSimpleName());
    service = service_class.newInstance();
    FragmentTransaction transaction = fm.beginTransaction();
    transaction.add(service, service_name);
    transaction.commit();
    fm.executePendingTransactions();
  }
  return service;
}</pre>

注：executePendingTransactions()是为了确保service对象在返回给调用者之前完成基本的初始化生命周期。

在Activity或其它Fragment中需要用到前台服务时，调用上述静态方法即可，它会保证在整个Activity生命周期内只有一份服务实例，因此我们直接使用前台服务的Class本身作为其标识。调用中需要传入的另一个参数『FragmentManager』，在FragmentActivity中可以通过getSupportFragmentManager()得到；在Fragment中可以通过getFragmentManager()获得。

考虑到Fragment的被动生命周期随Activity的销毁而终止，而App的Activity生命周期通常是短暂的，因此就不必引入『引用计数』之类的复杂机制来维护前台服务的终止时机了。

### （2）UI元素与前台服务之前的交互

从UI元素访问前台服务，可以简单的直接使用获取到的服务实例，调用其中的方法。服务实例的引用可以安全的保存在同源的Activity或Fragment对象中，但切忌不可保存在比父Activity生命周期更长的对象中，如静态成员中。

反过来，从前台服务访问UI元素，则稍有一些考究。对Activity的访问是最简单的，直接使用getActivity()方法即可得到所在的Activity实例，因此我们可以方便的将前台服务的处理过程借助Activity界面的『进度圆圈』（Indeterminate Progress）给用户友好的指示。对其它Fragment的访问，官方文档中提到了使用setTargetFragment()及getTargetFragment()实现，但放在前台服务的场景中，尤其是考虑到共享、解耦、并发等问题，这并不是一个好的方案。或许大部分开发者更容易联想到『回调模式』，比如在前台服务类中提供回调注册接口，这当然也不失为一个可行的方案，但个人更倾向使用灵活易用的LocalBroadcastManager实现服务往UI方向的通知。关于这个机制，这里就不引申介绍了，感兴趣的朋友可以直接看看Android Support Library的Javadoc。

### （3）实现跨状态切换的服务保持

前台服务由于不直接涉及界面布局，因此完全不必在屏幕旋转等状态切换中重建，从而有效降低这一过程中的体验延迟。实现上，其实非常简单，只需要在Fragment的初始化过程中将自身设定为『可保持』：

<pre>@Override public void onCreate(final Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  <strong>setRetainInstance(true);</strong>
}</pre>

### （4）与Loader机制的配合使用

Loader机制也是Android 3.0中增加的一个实用的辅助机制，可以帮助开发者更好的实现异步IO与UI组件的协同。与（同进程的）Service机制一样，前台服务的入口代码也是在主线程（UI线程）中执行的，因此必须尽可能避免在其中执行IO操作。借助Loader机制，可以很好的将IO，尤其是网络访问隔离到独立的工作线程中，同时兼顾与UI组件的便捷协同，因此前台服务与Loader机制可谓是一对绝佳的搭档。但在实际搭配使用中，也有一些需要注意的细节，如果使用不当也可能造成一些很难排查的异常。

使用LoaderManager时，需要明确区分是希望使用Activity级别的LoaderManager还是本Fragment（前台服务）级别的LoaderManager，不同于FragmentManager的统一性，它们其实是两个不同的实例，有着不一样的影响。大多数情况下，Loader仅限这个前台服务使用，因此使用Fragment级别的LoaderManager是最佳的选择。如果希望在多个前台服务之间复用某些Loader（例如CursorLoader），则须使用Activity级别的LoaderManager，但同时应小心避免Loader ID的冲突。

&nbsp;

以上是对前段时间基于Fragment所实现的前台服务框架初步探索的一个总结，这个机制已经在我最近开发的一个App中正常运作了一段时间，期间并未发现显著的问题或制肘。如果各位在借鉴上述机制的过程中遇到了任何疑惑和苦难，欢迎与我交流探讨。后续相关的经验和技巧，我也会在本文中补充完善。

附：ServiceFragment抽象基类的完整代码

<pre>public abstract class ServiceFragment extends Fragment {

  private static final String KServiceTagPrefix = "service:";

  @Override public void onCreate(final Bundle state) {
    super.onCreate(state);
    setRetainInstance(true);
  }

  /** @see {@link android.support.v4.content.LocalBroadcastManager#sendBroadcast(Intent)} */
  protected boolean sendLocalBroadcast(final Intent intent) {
    return LocalBroadcastManager.getInstance(getActivity()).sendBroadcast(intent);
  }

  public static &lt;T extends ServiceFragment&gt; T getService(final Class&lt;T&gt; service_class, final FragmentManager fm) {
    if (fm == null) throw new IllegalArgumentException("FragmentManager is null");
    final String service_name = KServiceTagPrefix + service_class.getCanonicalName();
    @SuppressWarnings("unchecked") T service = (T) fm.findFragmentByTag(service_name);
    if (service == null) {
      Log.i(TAG, "Starting service: " + service_class.getSimpleName());
      try {
        service = service_class.newInstance();
      } catch (final java.lang.InstantiationException e) {
        throw new IllegalArgumentException(service_class + " cannot be instantiated");
      } catch (final IllegalAccessException e) {
        throw new IllegalArgumentException(service_class + " is inaccessible");
      }
      final FragmentTransaction transaction = fm.beginTransaction();
      transaction.add(service, service_name);
      transaction.commit();
      fm.executePendingTransactions();
    }
    return service;
  }

  private static final String TAG = ServiceFragment.class.getSimpleName();
}</pre>