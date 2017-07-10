---
title: 清除
date: 2017-7-10
tags: [浏览器兼容]
categories: CSS
---
CSS常见兼容性问题总结

原文 http://www.cnblogs.com/imwtr/p/4340010.html

浏览器的兼容性问题，通常是因为不同的浏览器对同一段代码有不同的解析，造成页面显示不统一的情况。这里谈到的浏览器，主要指IE6/IE7/IE... FireFox Chrome Opera Safari 等。 但更多的兼容还是考虑IE6/IE7/FF之间的斗争先来谈谈CSS Hack我们为了让页面形成统一的效果，要针对不同的浏览器或不同版本写出对应可解析的CSS样式，所以我们就把这个针对不同浏览器/版本而写CSS的过程叫做 CSS hack.

## CSS hack
主要有三种：IE条件注释法、CSS属性前缀法、选择器前缀法。

### IE条件注释法
即在正常代码之外添加判别IE浏览器或对应版本的条件注释，符合条件的浏览器或
者版本号才回执行里边的代码。

```
<!--  lt是小于 gt是大于 lte是小于等于 gte是不小于 !是不等于 -->
<!-- [if IE]>
	你想要执行的代码 
<![endif]-->
<!-- [if lt IE 8]>
	你想要执行的代码 
<![endif]-->
<!-- [if ! IE 8]>
	你想要执行的代码 
<![endif]-->

```


### CSS属性前缀法
即是给css的属性添加前缀。比如 \* 可以被IE6/IE7识别，但 _ 只能被IE6识别，IE6-IE10都可以识别 "\9"，IE6不能识别!important  FireFox不能识别\* _ \9可以先使用“\9"标记，将IE分离出来，再用”*"分离出IE6/IE7，最后可以用“_”分离出IE6

```
.type{
	color: #111; /* all */

	color: #222\9; /* IE */
	*color: #333; /* IE6/IE7 */
	_color: #444; /* IE6 */
	}
```

所以可以按着优先级就能给特定的版本捎上特定颜色一般来说，只有IE6不支持 !important 所以可以这样

```
#example{
    width: 100px !important; /* IE7  FF */
    width: 110px; /* IE6 */
}
```

因为!important 具有最高优先级，所以此种方式可以区别出来~为什么说一般呢...你看看下面这个例子，IE6貌似还认得出!important

   
```
h1{color: #f00 !important; }
h1{color: #000;}
h2{color: #f00 !important; color: #000;
<h1>test1</h1>
<h2>test2</h2>
```


### 选择器前缀法，顾名思义，就是给选择器加上前缀

IE6可识别 *div{color:red;}  
IE7可识别 *+div{color:red;}

### 其它兼容问题

1. 最主要也是最常见的，就是浏览器对标签的默认支持不同，所以我们要统一，就要进行CSS reset . 最简单的初始化方法是 *{margin:0; padding:0;},但不推荐，而且它也并不完善。

贴一个淘宝的样式初始化~

    body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
        body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
        h1, h2, h3, h4, h5, h6{ font-size:100%; }
        address, cite, dfn, em, var { font-style:normal; }
        code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
        small{ font-size:12px; }
        ul, ol { list-style:none; }
        a { text-decoration:none; }
        a:hover { text-decoration:underline; }
        sup { vertical-align:text-top; }
        sub{ vertical-align:text-bottom; }
        legend { color:#000; }
        fieldset, img { border:0; }
        button, input, select, textarea { font-size:100%; }
        table { border-collapse:collapse; border-spacing:0; }

2. IE6双边距bug:块属性标签添加了浮动float之后，若在浮动方向上也有margin值，则margin值会加倍。其实这种问题主要就是会把某些元素挤到了第二行

```
<style type="text/css">
	html,body,div{ margin: 0;padding: 0;}
	.wrap{width: 200px; height: 200px; border: 1px solid #333;}
	.box{float: left; /* display:inline */ ;margin-left: 10px; width: 80px; height: 80px; background-color: green;}
	</style>
</head>
<body>
<div class="wrap">
	<div class="box"></div>
	<div class="box"></div>
</div>
<script type="text/javascript">
</script>
</body>
```


3. IE6下左边的双边距 ~

IE7的没问题          ~

解决的方式有两个：

- 给float元素添加display：inline 即可正常显示

- 就是hack处理了，对IE6进行 _margin-left:5px;

4. 跟上述差不多，也属于IE6双边距bug:
行内属性标签，为了设置宽高，我们经常就会设置成display：block; 这样一来就产生上述的问题。
解决办法也是isplay：inline;但是这样一来我们就不能设置宽高了，所以呢需要再加个display:table.所以你设置display:block后，再添上display:inline和display:table

5. 上下margin重合问题，相邻的两个div margin-left margin-right 不会重合，但相邻的margin-top margin-bottom会重合。

```
.box1{width: 200px;height: 200px; border: 1px solid #333; }
    .mt{margin-top: 10px;}
    .mb{margin-bottom: 10px;}

<div class="box1 mb"></div>
<div class="box1 mt"></div>
```
解决办法就是不要同时采用top和bottom ,统一一些~

6. 有些浏览器解析img标签也有不同，img是行内的，一般都会紧接着排放，但是在有些情况下还是会突然出现个间距，解决办法是给它来个浮动float 
7. 标签属性min-height是不兼容的，所以使用的时候也要稍微改改。

```
.box{min-height:100px;height:auto !important; height:100px; overflow:visible;}
```
另一方面，IE是不支持min-height这类属性的，所以有些时候也可以考虑使用CSS表达式

```
#container{ 

    min-width:600px;
    width: expression(document.body.clientWidth < 600? "600px":"auto");
}
```

8. 很多时候可能会纳闷超链接访问过后样式就混乱了，hover样式不出现了。其实主要是其CSS属性的排序问题。一般来说，最好按照这个顺序：L-V-H-A 

简单的记法是  love  hate 


```
a:link{}  a:visited{}  a:hover{}  a:active{}
```


9. chrome下默认会将小于12px的文本强制按照12px来解析。解决办法是给其添加属性：


```
-webkit-text-size-adjust: none;
```
 

10. png24位的图片在IE6下面会出现背景，所以最好还是使用png8格式的

11. 因为存在两种盒子模式：IE盒子模式和W3C标准模式，所以对象的实际宽度也要注意。

IE/Opera：对象的实际宽度 = (margin-left) + width + (margin-right)Firefox/Mozilla：对象的
实际宽度= (margin-left) + (border-left-width) + (padding- left) + width + (padding-right) + 
(border-right-width) + (margin-right)

12. 鼠标的手势也有问题：FireFox的cursor属性不支持hand，但是支持pointer，IE两个都支持；所以为了兼容都用pointer

13. 消除ul、ol等列表的缩进时，样式应写成:

```
list-style:none;margin:0px;padding:0px;
```
 其中margin属性对IE有效，padding属性对FireFox有效

14. CSS控制透明度问题：一般就直接 opacity: 0.6 ; IE就 filter: alpha(opacity=60)但在IE6下又有问题，所以又得弄成 filter:progid:DXImageTransform.Microsoft.Alpha(style=0,opacity=60);

15. 有些时候图片下方会出现一条间隙，通常会出现在FF和IE6下面比如
```
<div><img src="1.jpg"/></div>
```
一般给img添加vertical-align属性即可，比如top middle

```
img{verticle-align:center;}
```

16. IE6下div高度无法小于10px,比如定义一条高2px的线条，FF和IE7都正常但IE6就是10px解决的办法有两种：添加overflow属性或设置fontsize大小为高度大小  如：

```
<div style="height:2px;overflow:hidden;background:#000000;width:778px;"></div>

<div style="height:2px;font-size:2px;background:#000000;width:778px;">&nbps;</div>
```