---
title: Android Ramp Up 笔记
categories: 技术
date: 2018-09-11 10:40:21
tags:
---

#### MVP Pattern

- Model-View-Presenter
- 是由 `MVC` 演变而来。在 `MVP` 中：
  - `View` 更加专注于处理数据可视化和页面交互
  - `Model` 更加专注于数据的处理
  - `Presenter` 则提供 `View` 和 `Model` 之间数据的纽带，用于交互和数据传输
- **`View`不直接与`Model`交互**

> [MVP 设计模式理解，实战理解MVP](https://blog.csdn.net/u011418943/article/details/69840880)
>
> [Android MVP 详解（上）](https://www.jianshu.com/p/9a6845b26856)



#### RxJava/RxAndroid

- `RxJava` 的本质可以压缩为**异步**这一个词。说到根上，它就是一个实现异步操作的库，而别的定语都是基于这之上的。

- 优势：**简洁**

- `RxJava` 的异步实现，是通过一种扩展的**观察者模式**来实现的。

- `RxJava` 有四个基本概念：**Observable** (可观察者，即被观察者)、 **Observer** (观察者)、**subscribe** (订阅)、**事件**。

- `RxJava` 的观察者模式大致如下图：

  ![img](https://upload-images.jianshu.io/upload_images/2405826-1b43cf8a80bfca3f.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/599/format/webp)

> [Rxjava、RxAndroid系列](https://www.jianshu.com/p/10d4d7c69345)



#### Retrofit

- `Retrofit` 是 Square 的一个著名的**网络请求库**。
- `Retrofit` 除了提供了传统的 Callback 形式的 `API`，还有 `RxJava` 版本的 Observable 形式 `API`。



#### Robolectric



#### Android

- 构成应用的组件主要有四种：`Activities`活动、`Services` 服务、`Broadcast Receivers` 广播接收器 和 `Content Providers` 内容提供者。

- `Android Manifest` 用于向 Android 框架**注册组件**。

- `Activity`：Single focused thing that the user can do.(用户可以执行的单一任务)

  - 负责**显示应用用户界面**。

  - `Activity` 通过读取 `XML布局文件` 确定要创建哪些视图（并放在何处）。

  - > [Android 布局入门](https://classroom.udacity.com/courses/ud851/lessons/93affc67-3f0b-4f9b-b3a4-a7a26f241a86/concepts/cdbfd437-de24-4903-8f01-37c29427cb38#)

- `Layout` 

  - 分为三种：`FrameLayout` 帧布局、 `LinearLayout` 线性布局、 `ConstraintLayout` 约束布局





#### 大坑

##### Android Studio `Gradle Sync Failed` 错误 

- 出现错误的原因：**Android Studio 需要设置代理 FQ**
  - `settings` 搜索 `proxy` 

  - 我是用 ShadowSocks ，设置如下图：

    ![Proxy Setting](../../images/AndroidStudioProxy.png)

  > [【Android】给Android Studio设置代理](https://blog.csdn.net/lchad/article/details/43567675) 
