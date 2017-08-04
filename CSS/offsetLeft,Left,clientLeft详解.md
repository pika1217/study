---
title: 各种距离
date: 2017-7-6
tags: [宽高应用]
categories: CSS
---
#### clientWidth：可见窗口
**无padding、无滚动 ：** clientWidth = 盒子的width

**有padding、无滚动 ：** clientWidth = 盒子的width + 盒子的padding * 2

**有padding、有滚动 ：** clientWidth = 盒子的width + 盒子的padding * 2- 滚动轴宽度

clientTop = border-top

clientLeft = border-left
#### offsetWidth:元素自身

**无padding、无滚动、无border：** offsetWidth = clientWidth = 盒子的宽度

**有padding、无滚动、有border：** offsetWidth =
盒子的宽度 + 盒子padding*2 + 盒子边框*2 = clientWidth + 边框宽度*2

**有padding、有滚动，且滚动是显示的，有border：** offsetWidth = 盒子宽度 + 盒子padding*2 + 盒子边框*2 = clientWidth + 滚动轴宽度 + 边框宽度*2


#### scrollWidth:元素自身
**无滚动轴时：**
scrollWidth = clientWidth = 盒子宽度 + 盒子padding*2

**有滚动轴时：** scrollWidth = 实际内容的宽度 + padding*2
    scrollHeight = 实际内容的高度 + padding*2

    

参考：http://merrier.wang/?p=793
