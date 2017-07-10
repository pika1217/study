---
title: 伪元素
date: 2017-7-10
tags: [伪元素]
categories: CSS
---
****伪元素****
```
selector:pseudo-element {property:value;}
selector.class:pseudo-element {property:value;}
```
## ::first-line伪元素
>用于向文本的首行设置特殊样式
```
p:first-line
  {
  color:#ff0000;
  font-variant:small-caps;
  }
```
## ::first-letter伪元素
>用于向文本的首字母设置特殊样式
```
p:first-letter
  {
  color:#ff0000;
  font-size:xx-large;
  }
```
上述两类只能用于块元素
## 伪类和伪元素配合
```
p.article:first-letter
  {
  color: #FF0000;
  }
```
#### ::before 伪元素
> 在元素的内容前面插入新内容。
#### ::after 伪元素
> 在元素的内容后面插入新内容。


属性 |	描述 	
---|---
::first-letter |	向文本的第一个字母添加特殊样式。 
::first-line |	向文本的首行添加特殊样式。 	
::before |	在元素之前添加内容。 	
::after |	在元素之后添加内容。
::selection(CSS3新增) | 给选中文本添加效果