## 窗口位置
确定窗口相对屏幕内左上角左边和上边的位置，火狐属性screenX，screenY，其它浏览器screenLeft，screenTop
```
vat leftPos = (typeof window.screenLeft=="number")?window.screenLeft:window.screenX;
var topPos = (typeof window.screenTop == "number")?window.screenTop:window.screenY;
```

## 窗口大小
浏览器窗口本身的尺寸

    window.outerWidth、window.outerHeight

页面视图区(减去边框宽度的大小),即视口的大小

    window.innerWidth、window.innerHeight
    也可以通过DOM提供页面可见区域的信息
    var pageWidth = window.innerWidth;
	var pageHeight = window.innerHeight;
	if(typeof pageWidth !="number"){
		if(document.compatMode == "CSS1Compat"){
			pageWidth = document.documentElement.clientWidth;
			pageHeight = document.documentElement.clientHeight;
		}else{
			pageWidth = document.body.clientWidth;
			pageHeight = document.body.clientHeight;
		}
	}
    
## 导航和打开新窗口
window.open();
四个参数
1. 要加载的url
2. 窗口目标（类似于iframe中的target）
3. 一个特性字符串，表示新窗口都显示哪些特性
4. 一个表示新页面是否取代浏览器历史记录中当前加载页的布尔值