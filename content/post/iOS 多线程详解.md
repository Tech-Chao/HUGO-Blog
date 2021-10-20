+++
author = "咸鱼"
title = "iOS 多线程详解"
date = "2021-10-15"
toc = true
comments = true
description = "iOS 多线程深入浅出 GCD NSThread NSOperation"
tags = [
    "多线程",
    "GCD",
    "NSThread",
    "NSOperation",
]
categories = [
    "iOS"
]
draft = true
+++

## 前言

何为多线程？在百科上面的解释：线程是操作系统能够进行运算调度的最小单位。它被包含在进程之中，是进程中的实际运作单位。在 iOS 中我们可以理解为进程就是我们启动的一个App，一个进程要想执行任务,必须至少有一条线程.而 App 启动的时候，系统会默认开启一条线程，也就是主线程（Main Thread）。

在开发中我们知道要将耗时任务放在子线程中执行，将耗时任务的结果放回到主线程中处理（涉及到界面更新等）。防止主线程因处理太多任务或者线程阻塞导致 App 卡顿，而这正是多线程的作用。

<!--more-->

下面列出了目前 iOS 中的多线程方案：

| 方案        | 简介                                                                                | 语言 | 线程生命周期 | 使用频率 |
| ----------- | ----------------------------------------------------------------------------------- | ---- | ------------ | -------- |
| pthread     | · 通用的多线程 API <br>·适用于 UNIX/LINUX/Windows <br>·跨平台\可移植<br>·使用难度大 | C    | 程序员管理   | 几乎不用 |
| NSThread    | ·使用更加面向对象<br>·简单易用、可直接操作线程对象                                  | OC   | 程序员管理   | 偶尔使用 |
| GCD         | ·充分利用设备多核<br>·旨在替代NSThread等线程技术                                    | C    | 系统管理     | 经常使用 |
| NSOperation | ·基于GCD封装<br>·较GCD多一些简单使用功能<br>·使用更加面向对象                       | OC   | 系统管理     | 经常使用 |

## pthread

pthread 是一套通用的多线程的 API，可以在Unix / Linux / Windows 等系统跨平台使用，使用 C  语言编写，需要程序员自己管理线程的生命周期，使用难度较大，我们在 iOS 开发中几乎不使用 pthread，但是还是可以了解一下的。 POSIX 线程（POSIX threads），简称 Pthreads，在 iOS 如果需要使用 pthread 需要导入头文件 `#include<pthread/pthread.h>`

```
#include<pthread/pthread.h>


```
