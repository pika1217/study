---
title: CSS3圆角
date: 2017-7-5
tags: [布局方式]
categories: CSS
---
## border-radius属性
每个圆角存在"水平半径"（horizontal radius）和"垂直半径"（vertical radius）。border-radius可以同时设置1到4个值。如果设置1个值，表示4个圆角都使用这个值。如果设置两个值，表示左上角和右下角使用第一个值，右上角和左下角使用第二个值。如果设置三个值，表示左上角使用第一个值，右上角和左下角使用第二个值，右下角使用第三个值。如果设置四个值，则依次对应左上角、右上角、右下角、左下角（顺时针顺序）border-radius: 15px 5px;border-radius还可以用斜杠设置第二组值。这时，第一组值表示水平半径，第二组值表示垂直半径。第二组值也可以同时设置1到4个值，应用规则与第一组值相同。

```
border-radius: 15px 5px / 3px;// 水平半径：15px 5px 15px 5px;垂直半径: 3px 3px 3px 3px
```


### 单个圆角的设置
除了同时设置四个圆角以外，还可以单独对每个角进行设置。对应四个角，CSS3提供四个单独的属性：
```
border-top-left-radius
border-top-right-radius
border-bottom-right-radius
border-bottom-left-radius
```
这四个属性都可以同时设置1到2个值。如果设置1个值，表示水平半径与垂直半径相等。如果设置2个值，第一个值表示水平半径，第二个值表示垂直半径

### 浏览器支持

IE 9+、Opera 10.5、Safari 5、Chrome 4和Firefox 4，都支持上述的border-radius属性。早期版本的Safari和Chrome，支持-webkit-border-radius属性，早期版本的Firefox支持-moz-border-radius属性。

目前来看，为了保证兼容性，只需同时设置-moz-border-radius和border-radius即可。
```
-moz-border-radius: 15px;
border-radius: 15px;
```
（注意：border-radius必须放在最后声明，否则可能会失效。）

另外，早期版本Firefox的单个圆角的语句，与标准语法略有不同。
```
-moz-border-radius-topleft（标准语法：border-top-left-radius）
-moz-border-radius-topright（标准语法：border-top-right-radius）
-moz-border-radius-bottomleft（标准语法：border-bottom-left-radius）
-moz-border-radius-bottomright（标准语法：border-bottom-right-radius）
```

摘自: 阮一峰大师的博客