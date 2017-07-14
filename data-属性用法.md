---
title: data*属性用法
date: 2017-7-15
tags: [data*属性]
categories: HTML
---
## 原生Js中data属性使用方法
### 读、写属性
1. 直接在HTML元素中写： <div id="test" data-age="24">Click Here</div>
2. 通过Js来操作：var test = document.getElementById('test');test.dataset.my = 'Byron';

HTML5中元素都会有一个dataset的属性，这是一个DOMStringMap类型的键值对集合，这个属性中只包含那些带data-\*属性,使用Js对其添加和读取操作有注意:
    
1. 获取自定义属性时去掉前缀data-
    
2. 属性名称中含有连字符时使用驼峰命名法（在HTML中自动转换成连字符形式），但是在CSS属性选择器中使用连字符形式。

### getAttribute、setAttribute与自定义属性关系
    
1. 自定义属性也能通过get、setAttribute方式读写，test.setAttribute('data-age',25);test.getAttribute('data-age')
2. dataset只是attribute的一个子集，get、setAttribute可以操作所有的dataset内容。
    
### 浏览器兼容性

    Internet Explorer 11+
    Chrome 8+
    Firefox 6.0+
    Opera 11.10+
    Safari 6+

## Jquery操作data属性

### 读取操作
$(this).data('key',value)、$(this).data('key'),去掉data-前缀，对应的是$(this).attr()
>data属性不仅能存基本类型的数值，还能存对象，JSon等等形式的数据。

    

