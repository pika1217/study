---
title: HTML5适配移动端
date: 2017-7-16
tags: [HTML5适配移动端]
categories: HTML
---
## 主流的四种方法

### CSS3媒体查询

#### 定义
媒体查询可以让我们根据设备显示器的特性（如视口宽度、屏幕比例、设备方向：横向或纵向）为其设定CSS样式，媒体查询由媒体类型和一个或多个检测媒体特性的条件表达式组成。媒体查询中可用于检测的媒体特性有 width 、 height 和 color （等）。使用媒体查询，可以在不改变页面内容的情况下，为特定的一些输出设备定制显示效果。

#### 位置       
媒体查询写在CSS样式代码的最后，CSS是层叠样式表，在同一特殊性下，靠后的的样式会重叠前面的样式
#### 写法

```
@media screen and (max-width:720px) and (min-width:320px){

      body{

       background-color:red;

       }

@media screen and (max-width:320px){

      body{

         background-color:blue;

       }

}
```
该段媒体查询的意思是：当设备屏幕宽度在320px——720px之间时，媒体查询中body的背景色（background-color:red;）会重叠之前的body背景色，当设备屏幕宽度在320px以下时，媒体查询中body的body背景色（background-color:blue;）会重叠之前的body背景色

### 百分比适配

用百分比做适配的方法是子元素相对于父元素的百分之多少，比如父元素的宽度为100px;设置子元素的宽度可为60%;这时子元素的宽为60px;如父元素的宽度改为200px时，这时子元素的宽就是120px; 所以可将body默认宽度设置为屏幕宽度（PC中指的是浏览器宽度），子孙元素按百分比定位（或指定尺寸）就可以了，这只适合布局简单的页面，复杂的页面实现很困难。

### 使用meta标签
```
<meta name="viewport content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no"/>
width=device-width:宽度等于当前设备的宽度
initial-scale=1：初始的缩放比例（默认为1）
maximum-scale=1：允许用户缩放到得最大比例（默认为1）
user-scalable=no：用户不能手动缩放

```
### 使用rem来做适配
使用方法：

1、JS方法

```
var html = document.querySelector(‘html‘);

var rem = html.offsetWidth / 7.5;

html.style.fontSize = rem + “px”;
```

2、CSS方法

在根元素(html)中定义了一个基本字体大小为62.5%（也就是10px。设置这个值主要方便计算，如果没有设置，将是以“16px”为基准 ）。

```
html {font-size: 62.5%;/*10 ÷ 16 × 100% = 62.5%*/}

body { font-size: 1.4rem; /*1.4 × 10px = 14px */}

h1 {font-size: 2.4rem; /*2.4 × 10px = 24px*/}
```
