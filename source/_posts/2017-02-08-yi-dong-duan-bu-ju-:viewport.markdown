---
layout: post
title: "移动端布局：viewport"
date: 2017-02-08 22:46:51 +0800
comments: true
categories: 
- css
---

> 在移动设备上进行页面布局，必备的就是 viewport 的设置。

<!--more-->

## viewport 是什么

viewport 就是一个窗口，手机浏览器通过这个窗口显示页面。

这时 viewport 可能大于或小于页面，虽然可以通过手指缩放，但是会带来不良的用户体验。

![](../images/20170208105542.png)

在这个图中，不管是左边还是右边，都需要缩放，才能良好阅读，用户体验极差。

左边的情况可能使用了 % 作为单位，右边的则是正常布局，页面宽度超过 viewport 的宽度。

## viewport 属性

![](../images/2017020880814.png)

    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width"/>

## viewport 的 width 属性

我们在移动端布局页面时，可能都会碰到：有时忘记加 viewport，在手机上的布局元素会变得非常小。这是因为 viewport 的 width 属性。

首先要知道，viewport 的默认宽度是 980px。而我们布局页面时，往往是以逻辑像素为基准的。

以 iphone 6 为例，它的宽的逻辑像素是 375px，如果忘记设置 viewport，浏览器实际的宽会是 980px，扩大了将近 3 倍。此时，如果我们还按逻辑像素布局，放下的盒子就会变为预想的 1/3。

而我们将 width=device-width 后，就会解决这个问题。

<br/>

<< [上一篇：移动端页面布局：单位](http://www.cutwenty.com/blog/2017-02-08-shou-ji-she-bei-dan-wei-:dpi,-dp,-px.html)

\>> 下一篇：没有了
