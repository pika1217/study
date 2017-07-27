---
title: javaScript常见内存泄露原因
date: 2017-7-27
tags: 内存泄露
categories: javaScript
---
1. 全局变量引起内存泄露
2. 闭包引起内存泄露
3. dom清空或删除时，事件未清除导致的内存泄露
4. dom子元素存在引用引起内存泄露
5. 被遗忘的定时器和回调函数(其中有引用dom节点之类的)