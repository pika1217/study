---
title: cookie、localStorage、sessionStorage的区别
date: 2017-7-23
tags: 存储
categories: 前端综合
---
#### cookie、localStorage、sessionStorage的区别

LocalStorage（本地存储）和sessionStorage（会话存储） 是HTML5 Web Storage API 提供的，这两种方式都允许开发者使用js设置的键值对进行操作，在在重新加载不同的页面的时候读出它们。这一点与cookie类似。

1. 数据的生命期：cookie一般由服务器生成，在浏览器端保存，可设置失效时间。如果在浏览器端生成Cookie，默认是关闭浏览器后失效；localStorage除非被清除，否则永久保存；sessionStroage仅在当前会话下有效，关闭页面或浏览器后被清除;

2. 存放数据大小:cookie:4K左右;localStorage和sessionStorage一般为5MB；

3. 与服务器端通信：cookie每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题；localStorage和sessionStorage仅在客户端（即浏览器）中保存，不参与和服务器的通信

3. 易用性：cookie需要程序员自己封装，源生的Cookie接口不友好；localStorage和sessionStorage源生接口可以接受，亦可再次封装来对Object和Array有更好的支持
