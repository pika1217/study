---
title: react生命周期
date: 2017-8-17
tags: react
categories: react
---
## 状态
react组件的生命周期有三种状态：
1. Mounting：已插入真实DOM
2. Updating：正在被重新渲染
3. Unmounting：已移除真实DOM

## 方法
函数|描述
--|--
componentWillMount|在渲染前调用，在客户端也在服务端
componentDidMount|只在第一次渲染的时候调用，只在客户端
componentWillReceivePros|在组件接收到一个新的props时被调用，这个方法在初始化render时不会被调用
shouldComponentUpdate|返回一个布尔值，在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。
componentWillUpdate|组件接收到新的props或者state但是没有render时调用，初始化时不会被调用
componentDidUpdate|组件更新后立即调用，在初始化时不会调用
componentWiilUnmount|在组件从DOM中移除时立即调用