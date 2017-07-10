---
title: 伪类
date: 2017-7-10
tags: [伪类]
categories: CSS
---
****伪类语法****
```
selector : pseudo-class {property: value}
```
****CSS 类也可与伪类搭配使用****
```
selector.class : pseudo-class {property: value}
```
****锚伪类****
```
a:link {color: #FF0000}		/* 未访问的链接 */
a:visited {color: #00FF00}	/* 已访问的链接 */
a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
a:active {color: #0000FF}	/* 选定的链接 */
```
****first-child类****
```
p:first-child {font-weight: bold;}
li:first-child {text-transform:uppercase;}
```
>第一个规则将作为某元素第一个子元素的所有 p 元素设置为粗体。第二个规则将作为某个元素（在 HTML 中，这肯定是 ol 或 ul 元素）第一个子元素的所有 li 元素变成大写。

属性| 描述
---|---
:active |	向被激活的元素添加样式。 	
:focus |	向拥有键盘输入焦点的元素添加样式。 	
:hover |	当鼠标悬浮在元素上方时，向元素添加样式。 
:link |	向未被访问的链接添加样式。 
:visited |	向已被访问的链接添加样式。 	
:first-child |	向元素的第一个子元素添加样式。 	

>注：
```
p:first-child //选择所有元素的子元素中第一个p元素
p > i:first-child //选择所有p元素的子元素中的第一个i元素
p:first-child i //  选择所有作为第一个子元素的 <p> 元素中的所有 <i> 元素
p:nth-type-of(n) //匹配是p元素的父元素的第 n 个p子元素
```

#### css3新增伪类


2、CSS3新增伪类

新增伪类 |	作用
---|---
p:first-of-type | 选择每个含有<p>元素作为直接子元素的父元素的子元素中首个<p>元素。
p:last-of-type | 选择每个含有<p>元素作为==直接子元素==的父元素的子元素中的最后一个个<p>元素。
p:only-of-type| 选择每个含有唯一一个<p>元素作为直接子元素的其父元素下的唯一的那个<p>元素。
p:only-child| 选择==后代元素==中只有一个<p>元素的元素唯一的子元素<p>元素。

p:nth-child(n)|	先选择每个p元素的直接父元素，再选择每个父元素其下的第n个子元素，若子元素是p元素则选中。n可以是数字，表达式，奇偶

p:nth-last-child(n)|选择属于其父元素的倒数第n个子元素的每个<p>元素。
p:nth-of-type(n)| 先选择每个p元素的直接父元素，再选择每个父元素下的第n个p子元素，如果有则选中。n可以是数字，表达式，奇偶
p:nth-last-of-type(n) |选择属于其父元素倒数第n个<p>元素的每个<p>元素。
p:last-child|选择属于其父元素最后一个子元素的每个<p>元素。
p:empty|选择没有子元素的每个<p>元素（包括文本节点）。
p:target |选择当前活动的<p>元素。
:not(p)|选择非<p>元素的每个元素。
:enabled|控制表单控件的可用状态。
:disabled |控制表单控件的禁用状态。
:checked |单选框或复选框被选中。
