---
title: call、apply、bind
date: 2017-7-14
tags: [call、apply、bind]
categories: javaScript
---
## call，apply，bind
这三个方法其实都是继承自Function.prototype中的，属于实例方法。如果call,apply方法没有参数，或者参数为null或undefined或者this，则等同于指向全局对象


## 区别
方法 |	是否直接执行函数 |	传入的参数 |	调用方式
---|---|---|---
call |	是 | 	(context,arg1,arg2,arg3...) 第二个参数之后都是实参|function.call(context,arg1,arg2,arg3...)
apply |	是 	|(context,[arg1,arg2,arg3...])第二个参数必须是数组|function.apply(context,[arg1,arg2,arg3...])
bind |	否 	|(context)只有一个参数|var newFunction = function.bind(context);newFunction(arg1,arg2,arg3...)


a：第一个参数都是指定函数内部中this的指向（函数执行时所在的作用域），然后根据指定的作用域，调用该函数。

b：都可以在函数调用时传递参数。call，bind方法需要直接传入，而apply方法需要以数组的形式传入。

c：call，apply方法是在调用之后立即执行函数，而bind方法没有立即执行，需要将函数再执行一遍。


## 实例：

1、call
	

```
var a = {x: 1}; var b = function (y, z) { console.log(this.x + y + z) }; b.call(a, 3, 4);
//此时b的this（即b执行时的上下文）被改变为a，因此this.x为1，第二个参数之后都是传给b实参。
```


2、apply
	

```
var a = {x: 1}; var b = function (arr) { console.log(this.x + arr[0] + arr[1]) }; b.call(a, [3, 4]);
//此时b的this（即b执行时的上下文）被改变为a，第二个参数是一个数组
```


3、bind
	

```
var a = {x: 1}; var b = function (y, z) { console.log(this.x + y + z) }; var newB = b.bind(a);
//此时b的this（即b执行时的上下文）被改变为a，由此生成一个新函数，函数不会立即执行。 newB(3, 4);//函数此时才执行
```


## 常用场景

1、数组之间追加
	
   
```
var array1 = [12, "foo", {name: "Joe"}, -2458]; var array2 = ["Doe", 555, 100]; Array.prototype.push.apply(array1, array2); /* array1 值变为 [12 , "foo" , {name:"Joe"} , -2458 , "Doe" , 555 , 100] */ View Code
```


2、获取数组中的最大值和最小值

```
var numbers = [5, 458, 120, -215]; var maxInNumbers = Math.max.apply(Math, numbers); //458 View Code
```

3、验证是否是数组（前提是toString()方法没有被重写过）

```
function isArray(obj){ return Object.prototype.toString.call(obj) === '[object Array]'; }
```

>原生的Object.prototype.toString()与数组的toString()方法是有区别的，数组（引用）是继承Object，也是通过Object.prototype实现的，而toString（）就是Object.prototype中自带的方法，理论上会被Array对象继承，然而Array.prototype重写了toString（）方法，数组调用toString（）会返回逗号连接成的字符串。RegExp类型以及Date类型的toString()方法都被重写

4、类（伪）数组使用数组方法

```
var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*")); 
```


5、数字求和
	
 
```
function sum() { var numberSum = Array.prototype.reduce.apply(arguments, [function (prev, next) { return prev + next; }]); console.log(numberSum); } sum(1, 2, 3);
```


jQuery中$.type()函数判断对象类型的实现就是如下，通过Object.prototype.toString.call()返回[object,class],再截取出class

```
function type(boj){

       return Object.prototype.toString.call(boj).slice(8,-1);
}
```

在toString(this)方法被调用时,会执行下面的操作步骤:

    如果this的值为undefined,则返回"[object Undefined]".
    如果this的值为null,则返回"[object Null]".
    让O成为调用ToObject(this)的结果.
    让class成为O的内部属性[[Class]]的值.
    返回三个字符串"[object ", class, 以及 "]"连接后的新字符串.



参考：

http://www.cnblogs.com/EnSnail/p/6687491.html

https://www.zhihu.com/question/40892203/answer/93261099

http://www.cnblogs.com/libin-1/p/5823025.html