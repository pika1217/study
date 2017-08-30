---
title: Doctype
date: 2017-8-22
tags: HTML
categories: HTML
---
一、什么是DOCTYPE
DOCTYPE是Document Type（文档类型）的简写，在页面中，用来指定页面所使用的XHTML（或者HTML）的版本。要想制作符合标准的页面，一个必不可少的关键组成部分就是DOCTYPE声明。只有确定了一个正确的DOCTYPE，XHTML里的标识和CSS才能正常生效。

二、DOCTYPE的规则
DOCTYPE声明的写法遵循一定的规则，它指出阅读程序应该用什么规则集来解释文档中的标记。在Web文档的情况下，“阅读程序”通常是浏览器或者校验器这样的一个程序，“规则”则是w3c所发布的一个文档类型定义（dtd）中包含的规则。
每个dtd都包括标记、attributes、properties等内容，它们用于标记web文档的内容；此外还包括一些规则，它们规定了哪些标记能出现在其他哪些标记中。每个web建议标准（比如html 4 frameset和xhtml 1.0 transitional）都有自己的dtd。

三、选择什么样的DOCTYPE
如上例所示，XHTML 1.0中有3种DTD（文档类型定义）声明可以选择：过渡的（Transitional）、严格的（Strict）和框架的（Frameset）。这里分别介绍如下。

1．过渡的。
一种要求不很严格的DTD，允许在页面中使用HTML4.01的标识（符合xhtml语法标准）。过渡的DTD的写法如下：
引用

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```



2．严格的

一种要求严格的DTD，不允许使用任何表现层的标识和属性，例如
等。严格的DTD的写法如下：
引用

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```



3．框架的

一种专门针对框架页面所使用的DTD，当页面中含有框架元素时，就要采用这种DTD。框架的DTD的写法如下：
引用

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

转：http://www.linuxfly.org/post/391/



使用严格的DTD来制作页面，当然是最理想的方式。但是，对于没有深入了解Web标准的网页设计者，比较合适的是使用过渡的DTD。因为这种DTD还允许使用表现层的标识、元素和属性，比较适合大多数网页制作人员。