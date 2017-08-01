---
title: Flex布局
date: 2017-7-4
tags: [布局方式]
categories: CSS
---

#### Flex布局
###### flex布局
一个容器指定为flex布局：
   
```
.box{
      display: flex;
    }
```

行内元素也可以使用Flex布局。


```
.box{
  display: inline-flex;
}

.box{
  display: -webkit-flex; /* Safari chrome*/
  display: -moz-flex; /*firefox*/
  display: -ms-flex; /*ie*/
  display: flex;
}
```

注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

###### 基本概念
采用flex布局的元素称为容器，其所有子元素称为容器成员，即为flex项目，容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end。交叉轴的开始位置叫做cross start，结束位置叫做cross end。项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

#### 容器的属性
* ### flex-direction ### 
```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
row(默认值)：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```
* ### flex-wrap ###
``` 
    .box{
      flex-wrap: nowrap(不换行) | wrap(换行) | wrap-reverse(换行，第一行在下方);
    }
```
* ### flex-flow ###
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
```    
    .box {
      flex-flow: <flex-direction> || <flex-wrap>;
    }
```
* ### justify-content ###
justify-content属性定义了项目在主轴上的对齐方式。
```
    .box {
      justify-content: flex-start | flex-end | center | space-between | space-around;
    }
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```
* ### align-items ###
###### 定义项目在交叉轴上如何对齐。
```
    .box {
      align-items: flex-start | flex-end | center | baseline | stretch;
    }
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```
 * ### align-content ###
定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。多跟轴线就是当有换行的时候，属性会对每个项目起效果，比如流失布局的时候，固定每行多少个项目，多了就会换行，但是一定是紧贴着，这时候align-content就起效果了，align-content:flex-start;而align-items只会对第一行的项目起作用。 
```
    .box {
      align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    }
flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴
```
### 项目的属性
#### order 
定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```

    .item {
      order: <integer>;
    }

```
#### flex-grow
定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
```
    .item {
      flex-grow: <number>; /* default 0 */
    }

```
#### flex-shrink ####
定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
``` 
    .item {
      flex-shrink: <number>; /* default 1 */
    }

```
#### flex-basis
定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
``` 
    .item {
      flex-basis: <length> | auto; /* default auto */
    }

```
#### flex
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
``` 
    .item {
      flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    }
```
#### align-self
允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。。
``` 
    .item {
      align-self: auto | flex-start | flex-end | center | baseline | stretch;
    }
```
        


    
        
        


    
