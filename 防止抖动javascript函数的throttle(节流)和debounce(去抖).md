---
title: throttle(节流)和debounce(去抖)
date: 2017-7-19
tags: 性能优化
categories: 前端综合
---
## throttle
预先设定一个执行周期，当调用动作的时刻大于等于执行周期则执行该动作，然后进入下一个新周期。
    var last = 0 ;
    function throttle(fn,threshhold){
        return function(){
            var context = this;
            var args = arguments;
            var curr = +new Date();
            if(curr-last > threshhold){
                fn.apply(context,args);
                last = curr;
            }
        }
    }
例子:
       
```
var last = 0;
function throttle(fn,delay){
    return (function(){
    	var context = this;
    	var args = arguments;
    	var curr = new Date();				
    	if(curr - last > delay){
    		fn.apply(context,args);
    		last = curr;
    	}
    })();
}
object.onkeyup = function(){
	throttle(search,2000);
};
function search(){}
```

## debounce
当调用动作n毫秒后，才会执行该动作，若在这n毫秒内又调用此动作则将重新计算执行时间。
    
```
timer = null;
    function debounce(fn,delay){
    clearTimeout(timer)
        return function(){
            var context = this;
            var args = arguments;
            timer = setTimeout(function(){
                fn.apply(context,args);
            },delay);    
        }
    }
    $('input.username').keypress(debounce(function (event)
    {
    // do the Ajax request
    }, 250));
```
