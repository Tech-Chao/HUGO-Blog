+++
author = "咸鱼"
title = "iOS 性能优化——启动时间"
date = "2021-10-15"
toc = true
comments = true
description = "iOS开发 | App启动时间优化 "
tags = [
    "iOS 性能优化",
    "App 启动时间"
]
categories = [
    "iOS"
]
+++

> 本篇是 iOS 性能优化系列的第一篇，讲述关于 App 的启动时长的优化

## 前言

用户对于 App 的第一印象就是 App 的启动时长，如果 App 启动的时长过长对于用户的体验可想而知

在[WWDC 2019 Optimizing App Launch](https://developer.apple.com/videos/play/wwdc2019/423/)中的将 App 的启动分为冷启动（Cold）、热启动（Warm）和恢复启动（Resume）。

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/ios/Lanuch_Types.png)

- 冷启动（Cold）：系统刚重启后、应用没有在内存中、应用的进程并不在系统中，需要系统创建一个进程分配给它，这是一个完整的启动过程
- 热启动（Warm）： 应用刚刚结束、应用的部分资源还在内存中，应用进程不在系统中
- 复启动（Resume）：APP 没结束，只是暂停，全在内存中，进程也存在。

我们对 App 启动时长的优化一般针对的是 App 的冷启动时长优化，根据 WWDC 的介绍，如果我们将首屏的渲染时间降低到 400ms（系统启动动画时长） 以内，那么用户的体验将会有极大的提升。

接下来，让我们按步骤一步步来优化启动时长：

1. 了解App启动的各阶段任务
2. 分析各阶段任务的时长
3. 有针对性的优化每个步骤的时长


同时为了准确的测量 App 的启动时长，我们对测试环境有一定的要求：
- 重启手机并放置一段时间
- 设置飞行模式或采用 Mock 网络请求的方式来减少不稳定的网络影响测试数据
- 退出 iCloud 账号
- 使用 Release 的包进行测试
- 采用当前主流的设备，而不是最新或者是太久的手机

 

## 启动阶段分析

优化之前我们需要知道 App 启动时有哪些阶段，每个阶段都做了哪些事情，有哪些地方是我们可以优化的。

![](https://cdn.jsdelivr.net/gh/Tech-Chao/blog-images/ios/Phases_of_App_Launch.png)

以上6个阶段从系统初始化到 App 初始化，再到 UI 视图的创建和布局，还有 App 数据的异步加载等扩展功能,

### System Interface
在 System Interface 阶段时由操作系统控制，主要包含以下任务：
- 加载可执行文件（Mach-O格式）到内存空间
- 执行一系列动态链接操作,进行 rebase 指针调整和 bind 符号绑定；

Mach-O 文件类型主要分为：

- 中间对象文件（MH_OBJECT）
- 可执行二进制（MH_EXECUTE）
- VM 共享库文件（MH_FVMLIB）
- Crash 产生的 Core 文件（MH_CORE）
- preload（MH_PRELOAD）
- 动态共享库（MH_DYLIB）
- 动态链接器（MH_DYLINKER）
- 静态链接文件（MH_DYLIB_STUB）符号文件和调试信息（MH_DSYM）这几种。
  

dyld 动态链接库也是 Mach-o 类型，所以会也会先加载到内存中 ，加载完后dyld会递归加载 App 依赖的动态库，然后执行符号绑定Rebase, Bind。一般应用会加载 100 到 400 个 dylib 文件，幸运是大部分是系统库，且系统会在操作系统启动时计算和缓存系统动态库。

### Runtime Init

- Objc 和 Swift 的初始化
  
  通过_dyld_objc_notify_register注册回调完成相关类的注册，在 image 加载完时初始化语言相关。

- 加载 category
 
    在上面语言初始化完之后，会加载所有 category，将 category 的所有方法，协议和属性加载到对应的主类中。

- 调用所有+load

    在 image 加载完时，通过load_images 触发，处理该 image 相关的所有+load 方法，按照继承层级依次调用：父类+load→子类+load→category +load，注意 category 的+load 不会覆盖原类。

- 调用 C++的构造函数属性函数 attribute((constructor)) 


### UIKit Init
- 实例化 UIApplication 和 UIApplicationDelegate
- 开始事件处理和系统集成
- Application Init
 
    - 这部分是我们熟悉的 UIApplicationDelegate 的几个生命周期调用：
    - application:willFinishLaunchingWithOptions:
    - application:didFinishLaunchingWithOptions:
    - applicationDidBecomeActive:
    - scene:willConnectToSession:options:
    - sceneWillEnterForeground:
    - sceneDidBecomeActive:

### Initial Frame Render

首页第一帧的渲染，包含了创建、布局和绘制视图的工作，并把准备好的第一帧提交给渲染层渲染，以下方面会被调用

```
loadView
viewDidLoad
layoutSubviews
```

### Extended

Extended 主要是一些扩展的任务，苹果给出的定义是在首屏显示后，App 响应用户的操作的同时，可能存在异步请求数据，等到数据返回后重新渲染首页。


## 各阶段优化


