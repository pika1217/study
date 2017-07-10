---
title: inline、block、inline-block之间的区别
date: 2017-7-3
tags: [inline,block]
categories: CSS
---
## inline
1. inline元素不会独占一行，多个相邻的行内元素在一行中排列，除非一行排列不下才会换一行，其高度随元素的内容而变化。
2. 设置width、height属性无效
3. 元素的margin、padding在水平方向会产生边距效果，但竖直方向不会。

## block
1. block元素独占一行，默认填满父元素宽度。
2. 可以设置width、height、margin、padding属性

## inline-block
1. 将对象呈现为内联对象，内容作为块级元素对象呈现，在同一行，可设置高宽，比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。

摘自：http://www.cnblogs.com/KeithWang/p/3139517.html 