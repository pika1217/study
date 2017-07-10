---
title: CSS3新特性
date: 2017-7-09
tags: [CSS3]
categories: CSS
---
##  CSS3的新特性整理

### animation    IE10+

animation的六大属性
    
####     animation-name
    规定需要绑定选择器的keyframe名称
    
####    animation-duration
规定完成动画所花费的时间 s ms ，object.style.animationDuration="3s"
    
####     animation-timing-function
动画的速度曲线，默认值ease，object.style.animationTimingFunction="linear"，语法 animation-timing-function:value

    animation-timing-function使用名为三次Cubic Bezier贝塞尔曲线函数的数学函数，来生成速度曲线 可以使用自己的值也可
    以预定义的值
    值:linear从始到末以相同的速度
    ease 默认 从低速 加快在结束前变慢
    ease-in动画低速开始
    ease-out动画低速结束
    ease-in-out动画从低速开始和结束
    cubic-bezier(n,n,n,n)在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值
    
    
####    animation-deplay
    
    动画开始之前的延迟
    animation-delay: time;
    JavaScript 语法：object.style.animationDelay="2s"
    animation-delay 值以秒或毫秒计。
    允许负值，-2s 使动画马上开始，但跳过 2 秒进入动画
    
     
    
####    animation-iteration-count
    
    动画播放的次数 IE10
    animation-iteration-count: n|infinite
    JavaScript 语法： object.style.animationIterationCount=3
   
####    animation-direction
    是否应该轮流反向播放动画
    animation-direction 值是 "alternate"，则动画会在奇数次数（1、3、5 等等）正常播放，而在偶数次数（2、4、6 等等
    ）向后播放
    animation-direction: normal|alternate;
    JavaScript 语法： object.style.animationDirection="alternate"
    
    
    默认值 none 0 ease 0 1 normal
    javascript的语法 object.style.animation="mymove 5s infinite"


```
div
{
width:100px;
height:100px;
background:red;
position:relative;
animation:mymove 5s infinite;
-webkit-animation:mymove 5s infinite; /*Safari and Chrome*/
}

@keyframes mymove
{
from {left:0px;}
to {left:200px;}
}

@-webkit-keyframes mymove /*Safari and Chrome*/
{
from {left:0px;}
to {left:200px;}
}
```

### Transition   过渡的四大属性 IE10+

#### transition-property

transiont-property属性规定过渡css属性的名称
transition-property: none|all|propertyCSS 属性名称列表，列表以逗号分隔;
JavaScript 语法： object.style.transitionProperty="width,height"


#### transition-duration
完成过渡效果需要多少秒或毫秒
transition-duration: time;
JavaScript 语法： object.style.transitionDuration="5s"


####  transition-timing-function:
linear|ease|ease-in|ease-out|ease-in-out|cubic-
bezier(n,n,n,n);
JavaScript 语法： object.style.transitionTimingFunction="linear"


####  transition-delay
JavaScript 语法： object.style.transitionDelay="2s"
transition-delay: time;

默认值 all 0 ease 0
transition:property duration timing-function delay
javascript语法：object.style.transition="width 2s"

```
div
{
width:100px;
height:100px;
background:blue;
transition:width 2s;
-moz-transition:width 2s; /* Firefox 4 */
-webkit-transition:width 2s; /* Safari and Chrome */
-o-transition:width 2s; /* Opera */
}

div:hover
{
width:300px;
}
```

 

 

#### transform IE10
transform 允许我们对元素进行旋转、缩放、移动、或倾斜
默认none
javascript的语法 object.style.transform="rotate(7deg)"
transform: none|transform-functions;

none 不进行转换
matrix(n,n,n,n,n,n)使用六个值的矩阵
matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)使用 16 个值的 4x4 矩阵
translate(x,y)2D 转换
translate3d(x,y,z)3D 转换
translateX(x)只是用 X 轴的值
translateY(y)只是用Y轴的值
translateZ(z)只是用Z轴的值
scale(x,y)2D缩放
scale3d(x,y,z)3D缩放
scaleX(x),scaleY(y),scaleZ(z)
rotate(angle) 2D 旋转，在参数中规定角度
rotate3d(x,y,z,angle)3D 旋转
rotateX(angle),rotateY(angle),rotateZ(angle)
skew(x-angle,y-angle) 定义沿着 X 和 Y 轴的 2D 倾斜转换
skewX(angle) skewY(angle) perspective(n)

 

新增的css3的选择器

```
1 E:nth-last-child(n) 
     2 E:nth-of-type(n) 
     3 E:nth-last-of-type(n) 
     4 E:last-child 
     5 E:first-of-type 
     6 E:only-child 
     7 E:only-of-type 
     8 E:empty 
     9 E:checked 
    10 E:enabled 
    11 E:disabled 
    12 E::selection 
    13 E:not(s)
    14 E::not(.s)
    15 body: nth-child(even), nth-child(odd)/*：此处他们分别代表了表格（tbody）下面的偶数行和奇数行（tr）*/等等......
```



 

#### @Font-face 特性
Font-face 可以用来加载字体样式，而且它还能够加载服务器端的字体文件，让客户端显示客户端所没有安装的字体


Font-face 客户端字体案例
<p><font face="arial">arial courier verdana</font></p>


Font-face 服务端字体案例


```
1 @font-face { 
 2 font-family: BorderWeb; 
 3 src:url(BORDERW0.eot); 
 4 } 
 5 @font-face { 
 6 font-family: Runic; 
 7 src:url(RUNICMT0.eot); 
 8 }
 9 
10 .border { FONT-SIZE: 35px; COLOR: black; FONT-FAMILY: "BorderWeb" } 
11 .event { FONT-SIZE: 110px; COLOR: black; FONT-FAMILY: "Runic" }
```



 

#### Word-wrap

设置或检索当当前行超过指定容器的边界时是否断开转行，文字此时已被打散Text-overflow它与 word-wrap 是协同工作word-wrap 设置或检索当当前行超过指定容器的边界时是否断开转行，而 text-overflow则设置或检索当当前行超过指定容器的边界时如何显示

1 .clip{text-overflow:clip; overflow:hidden; white-space:nowrap; 
2 width:200px;background:#ccc;} 
3 .ellipsis{text-overflow:ellipsis; overflow:hidden; white-space:nowrap; 
4 width:200px; background:#ccc;}

1 <div class="clip"> 不显示省略标记，而是简单的裁切条</div>
2 
3 <div class="ellipsis"> 当对象内文本溢出时显示省略标记</div>

 

文本渲染

1 div { 
2 -webkit-text-fill-color: black; 
3 -webkit-text-stroke-color: red; 
4 -webkit-text-stroke-width: 2.75px; 
5 }

Text-fill-color: 文字内部填充颜色
Text-stroke-color: 文字边界填充颜色
Text-stroke-width: 文字边界宽度

#### gradient 渐变效果
线性渐变 linear左上（0% 0%）到右上(0% 100%)

background-image:-webkit-gradient(linear,0% 0%,100% 0%,form(red),to(balck))

background-image:-webkit-gradient(linear,0% 0%,100% 0%,from(#2A8BBE),
color-stop(0.33,#AAD010),color-stop(0.33,#FF7F00),to(#FE280E));


径向渐变radial从一个圆到一个圆的渐变
background:-weblit-gradient(radial,50 50,50,50 50,0,form(black),color-stop(0.5,red),to(blue));


css3的阴影shadow和反射reflect

background-clip:border-box;背景从border开始显示；
background-clip：padding-box
background-clip：content-box
background-clip:no-clip:no-clicp默认属性等同于border-box


background-origin 用于确定背景的位置 通常与background-positon联合使用


background-size来调整背景图片的大小，注意别和 clip 弄混，这个主要用于设定图片本身

background-size: contain; 缩小图片以适合元素（维持像素长宽比）
background-size: cover; 扩展元素以填补元素（维持像素长宽比）
background-size: 100px 100px; 缩小图片至指定的大小 .
background-size: 50% 100%; 缩小图片至指定的大小，百分比是相对包 含元素的尺寸

 


background-break: continuous; 默认值。忽略盒之间的距离（也就是像元 素没有分成多个盒子，依然是
一个整体一 样）
background-break: bounding-box; 把盒之间的距离计算在内；
background-break: each-box; 为每个盒子单独重绘背景

 

counter()=[counter(name) | counters(name,list-style-type)]{1,}

counter-reset IE8

counter-reset 属性设置某个选择器出现次数的计数器的值。默认为 0。
利用这个属性，计数器可以设置或重置为任何值，可以是正值或负值。如果没有提供 number，则默认为 0。
注释：如果使用 "display: none"，则无法重置计数器。如果使用 "visibility: hidden"，则可以重置计数器

JavaScript 语法： object.style.counterReset="subsection"

counter-reset的值none id number inherit

 

attr()=attr(attr-name)插入元素的属性值 IE8


calc() =calc(四则运算) 动态计算长度值 IE9
需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；
calc()函数支持 "+", "-", "*", "/" 运算；
calc()函数使用标准的数学运算优先级规则；

initial属于css-wide关键字，这表示所有的属性都可以接受该值 IE11


unset 擦除属性声明

颜色值
color color的颜色名称，HEX，RGB，RGBA，HSL，HSLA，transparent,currentColor


currentColor

resolution分辨率值不允许有负值
频率单位包括有： dpi, dpcm, dppx

角度值 angle角度值的正常范围应在[0-360deg]内，例如：-10deg与350deg是等价的
角度单位包括有： deg, grad一个圆共400梯度, rad 一个圆共2π弧度, turn
90deg = 100grad = 0.25turn ≈ 1.570796326794897rad


#### 长度值与单位

    ch 数字“0”的宽度 ie9
    
    rem 相对长度单位。相对于根元素(即html元素)font-size计算值的倍数
    vw 相对于视口的宽度。视口被均分为100单位的vw ie9
    vh 相对于视口的高度。视口被均分为100单位的vh
    vmax 相对于视口的宽度或高度中较大的那个。其中最大的那个被均分为100单位的vmax
    vmin 相对于视口的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vmin
    q 1/4毫米（quarter-millimeters）。绝对长度单位。
    1in = 2.54cm = 25.4 mm = 101.6q = 72pt = 6pc = 96px

@import@media@font-face@keyframes@supports

 


CSS3 的盒子模型
盒子模型为开发者提供了一种非常灵活的布局方式，但是支持这一特性的浏览器并不多，目前只有 webkit 内核的新版本 safari 和 chrome 以及 gecko 内核的新版本 firefox