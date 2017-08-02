---
title: viewport
date: 2017-8-1
tags: CSS
categories: CSS
---
## layout viewport（布局视口）
一般移动设备的浏览器都默认设置了一个viewport 元标签，定义一个虚拟的layout viewport（布局视口），用于解决早期的页面在手机上显示的问题。iOS, Android基本都将这个视口分辨率设置为 980px，所以pc上的网页基本能在手机上呈现，只不过元素看上去很小，一般默认可以通过手动缩放网页。

## visual viewport（视觉视口）
visual viewport（视觉视口）指物理设备屏幕的可视区域，屏幕显示器的物理像素，同样尺寸的屏幕，像素密度大的设备，硬件像素会更多。

## ideal viewport（理想视口）和 dip （设备逻辑像素）
ideal viewport（理想视口）通常是我们说的屏幕分辨率。

dip （设备逻辑像素）跟设备的硬件像素无关的。一个 dip 在任意像素密度的设备屏幕上都占据相同的空间。

而移动端手机屏幕通常不可以设置分辨率，一般都是设备厂家默认设置的固定值，换句话说 dip 的值就是 ideal viewport（理想视口）

## CSS像素

CSS像素（px）用于页面布局的单位。样式的像素尺寸（例如 width: 100px）是以CSS像素为单位指定的。CSS像素与 dip 的比例即为网页的缩放比例，如果网页没有缩放，那么一个CSS像素就对应一个 dip（设备逻辑像素） 。

## 使用viewport元标签控制布局

首先看一下viewport元标签极其属性：

html 代码:

```
<meta id="viewport" name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1; user-scalable=no;">
```


这里是每个属性的详细介绍：

属性名 | 	取值 |	描述
--|--|--
width |	正整数 或 device-width 	|定义视口的宽度，单位为像素，即layout viewport的宽度
height |	正整数 或 device-height 	|定义视口的高度，单位为像素，一般不用
initial-scale |	[0.0-10.0] |	定义初始缩放值
minimum-scale |	[0.0-10.0] 	|定义缩小最小比例，它必须小于或等于maximum-scale设置
maximum-scale |	[0.0-10.0] 	|定义放大最大比例，它必须大于或等于minimum-scale设置
user-scalable |	yes/no 	|定义是否允许用户手动缩放页面，默认值yes