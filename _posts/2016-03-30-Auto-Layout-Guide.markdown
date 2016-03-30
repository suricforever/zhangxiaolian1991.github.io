---
layout: post
title:  "Auto Layout Guide"
date:   2016-03-30 14:53:08
categories: jekyll update
comments: false
---
# Auto Layout 编程指南

### 理解 Auto Layout

Auto Layout 会动态计算在 View hierarchy 中所有的 View 的大小和位置，并根据 contrainst 进行布局。例如，一个 button 在 imageView 上的 contrainst 为水平居中并且离顶部 8 个像素点的距离 ，当 imageView 的 size 或者 position 改变的时候，button 的 position 会动态的改变以适应前面设置的 contrainst。

Auto Layout 可以动态响应 **外部改变（External Changes）**和 **内部改变（Internal Changes）**。

#### 外部改变（External Changes）
当 superview 的 size 和 shape 发生改变时，会触发 **外部改变（External Changes）**。无论改变那个，都要 更新 view hierarchy 的 布局（layout）。以下是一些 **外部改变（External Changes）** 的例子:

* 改变窗口（window）的大小（OS X）
* 在iPad上 进入或者离开 Split View（iOS）
* 设备旋转 （iOS）
* 电话或录音的 bar 的出现或消失 （iOS）
* 支持不同的 Size Classes
* 支持不同的屏幕大小（iOS）

#### 内部改变（Internal Changes）

当内部的 View 或 control 的大小发生变化时，会触发 **内部改变（Internal Changes）**。以下是一些 **内部改变（External Changes）** 的例子

* app 显示的内容发生变化
* 国际化
* 支持动态类型（Dynamic Type）（iOS） 

#### Auto Layout Versus Frame-Based Layout

* 基于 Frame 的 编程布局
* AutoResize mask 自动适配外部变化
* 全新的Auto Layout 布局 基于约束