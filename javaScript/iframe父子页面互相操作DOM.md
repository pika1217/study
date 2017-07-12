---
title: iframe父子页面互相操作DOM
date: 2017-7-01
tags: [iframe]
categories: javaScript
---
## javaScript版本

>主要通过contentWindow对象以及window.parent

### 父页面获取子页面的方式

>iframe的contentWindow属性，代表iframe所在的window对象。 
       
      
```
//1. 获取iframe节点
        var iframe = document.getElementById('iframeId');
        或
        var iframe = frames['iframeId'];
        或
        var iframe = window.frames['iframeId'];
        或
        var iframe = iframeId;
        //2. 然后获取iframe包含的document对象:
        IE浏览器：
        var cWindow = iframe.document;
        其它浏览器：
        var cWindow = iframe.contentWindow.document;
        或
        var cWindow = iframe.contentDocument;
```


```
<script type="text/javascript">  
     
       //some other operation
    frames['iframeId'].onload = function () {
    var childDocument = this.contentDocument || this.document; 
    var div=childDocument.getElementById('divId'); 
    }  
    </script> 

<iframe id="iframeId" src="iframe.html" width="100" height="100"></iframe>

//子页面
<div id="divId"></div>

```

### 子页面获取父页面的方式

>通过window.parent获取

```
父页面
<div id-"pDivId"></div>
<iframe src="iframe.html" width="100" height="100"></iframe>

//子页面
<script type="text/javascript">  
    window.onload = function(){ 
        if (window.parent !== window.self) {
        //当前窗口是子窗口
        var parentDocument =window.parent.document;
        }
    var pDiv=parentDocument.getElementById('pDivId');  
       //some other operation
    }  
    </script>
```

## Jquery版本

>主要是通过

```
$(window.frames["iframeChild"].document).find() //父页面操作子页面
$(window.parent.document).find()
//子页面操作父页面
```

实质就是获取要操作的页面的document转换为Jquery对象
### 父页面操作子页面DOM

```
$(window.frames["iframeId"].document).find('#divId')
```


### 子页面操作父页面DOM

```
$(window.parent.document).find('#pDivId')
```


## iframe优缺点

### iframe的优点：

1. iframe能够原封不动的把嵌入的网页展现出来。
2. 如果有多个网页引用iframe，那么你只需要修改iframe的内容，就可以实现调用的每一个页面内容的更改，方便快捷。
3. 网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用iframe来嵌套，可以增加代码的可重用。
4. 如果遇到加载缓慢的第三方内容如图标和广告，这些问题可以由iframe来解决。
    
### iframe的缺点：

1. 会产生很多页面，不容易管理。
2. 会出现多个上下、左右滚动条，用户体验度差。
3. 现在的搜索引擎爬虫还不能很好的处理iframe中的内容，所以使用iframe会不利于搜索引擎优化。
4. 很多的移动设备（PDA 手机）无法完全显示框架，设备兼容性差。
5. iframe框架页面会增加服务器的http请求，对于大型网站是不可取的。
6. window 的 onload 事件需要在所有 iframe 加载完毕后(包含里面的元素)才会触发，延迟加载速度。
7. iframe在加载资源时可能用光了所有的可用连接，从而阻塞了主页面资源的加载。
分析了这么多，现在基本上都是用Ajax来代替iframe，所以iframe已经渐渐的退出了前端开发。

### iframe与frame的区别

1. frame不能脱离frameSet单独使用，iframe可以；
2. frame不能放在body中，嵌套在frameSet中的iframe必需放在body中；
3. 不嵌套在frameSet中的iframe可以随意使用；
4. frame的高度只能通过frameSet控制；iframe可以自己控制，不能通过frameSet控制。
5. 如果在同一个页面使用了两个以上的iframe，在IE中可以正常显示，在firefox中只能显示出第一个；使用两个以上的frame在IE和firefox中均可正常