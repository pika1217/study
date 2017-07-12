---
title: js中typeof与instanceof用法小记
date: 2017-7-01
tags: [typeof and instanceof]
categories: javaScript
---

## 判断一个对象
typeof用以获取一个变量或者表达式的类型，typeof一般只能返回如下几个结果：number,boolean,string,function（函数）,object（NULL,数组，对象）,undefined。
如：

```
alert(typeof (123));//typeof(123)返回"number"
alert(typeof ("123"));//typeof("123")返回"string"
```
我们可以使用typeof来获取一个变量是否存在，如if(typeof a!="undefined"){}，而不要去使用if(a)因为如果a不存在（未声明）则会出错，正因为typeof遇到null,数组,对象时都会返回object类型，所以当我们要判断一个对象是否是数组时或者判断某个变量是否是某个对象的实例则要选择使用另一个关键语法instanceof。

instanceof用于判断一个变量是否某个对象的实例，如

```
var a=new Array();alert(a instanceof Array);
```
会返回true，同时alert(a instanceof Object)也会返回true;这是因为Array是object的子类。再如：

```
function test(){};var a=new test();alert(a instanceof test)//会返回true。
```
也可以使用Object.prototype.toString.call()来判断数据类型，过程是
1、获取对象的类名（对象类型）。
2、然后将[object、获取的类名、]组合并返回。

```
console.log(Object.prototype.toString.call(123)) //[object Number]
console.log(Object.prototype.toString.call('123')) //[object String]
console.log(Object.prototype.toString.call(undefined)) //[object Undefined]
console.log(Object.prototype.toString.call(true)) //[object Boolean]
console.log(Object.prototype.toString.call({})) //[object Object]
console.log(Object.prototype.toString.call([])) //[object Array]
console.log(Object.prototype.toString.call(function(){})) //[object Function]

"Arguments", "Array", "Boolean", "Date", 
"Error", "Function", "JSON", "Math", "Number", 
"Object", "RegExp", "String"
```

## instanceof运算符定义是

```
function instance_of(L, R) {//L 表示左表达式，R 表示右表达式
 var O = R.prototype;// 取 R 的显示原型
 L = L.__proto__;// 取 L 的隐式原型
 while (true) { 
   if (L === null) 
     return false; 
   if (O === L)// 这里重点：当 O 严格等于 L 时，返回 true 
     return true; 
   L = L.__proto__; 
 } 
}
```

其中_proto_指向的是当前对象的原型对象，prototype指向它的构造函数的原型对象

```
Object.__proto__ = Function.prototype？答：true
function func(){}
func.__proto__ == Function.prototype;//true
Function.__proto__ == Function.prototype;//true
Array.__proto__ == Function.prototype;//true
Object.__proto__ == Function.prototype;//true
Function.prototype.__proto__ == Object.prototype;//true
Object.prototype.__proto__ == null//true
```

```
function Foo(){}
Foo.prototype = new Aoo();//JavaScript 原型继承
var foo = new Foo();
console.log(foo instanceof Foo)//true
console.log(foo instanceof Aoo)//true
```

上面的代码中是判断了一层继承关系中的父类，在多层继承关系中，instanceof 运算符同样适用。

又如：

```
console.log(Object instanceof Object);//true
console.log(Function instanceof Function);//true console.log(Number instanceof Number);//false
console.log(String instanceof String);//false
console.log(Function instanceof Object);//true
console.log(Foo instanceof Function);//true
console.log(Foo instanceof Foo);//false
```



```
1、Object instanceof Object
// 为了方便表述，首先区分左侧表达式和右侧表达式
ObjectL = Object, ObjectR = Object; 
// 下面根据规范逐步推演
O = ObjectR.prototype = Object.prototype 
L = ObjectL.__proto__ = Function.prototype 
//Console.log(Object) 为function Number()
// 第一次判断
O != L 
// 循环查找 L 是否还有 __proto__ 
L = Function.prototype.__proto__ = Object.prototype 
// 第二次判断
O == L 
// 返回 true
```




```
2、 Function instanceof Function
// 为了方便表述，首先区分左侧表达式和右侧表达式
FunctionL = Function, FunctionR = Function; 
// 下面根据规范逐步推演
O = FunctionR.prototype = Function.prototype 
L = FunctionL.__proto__ = Function.prototype 
// 第一次判断
O == L 
// 返回 true
```



```
3.Number instanceof Number
NumberL = Numebr,NumberR = Number
O = NumberR.prototype = Number.prototype
L = NumberL._proto_ = Function.prototype
//Console.log(Number) 为function Number()
O != L 
// 循环再次查找 L 是否还有 __proto__ 
L = Function.prototype.__proto__ = Object.prototype 
// 第二次判断
O != L 
// 再次循环查找 L 是否还有 __proto__ 
L = Object.prototype.__proto__ = null 
// 第三次判断
L == null 
// 返回 false
同理 Boolean String 都是false
```




```
4、Foo instanceof Foo
// 为了方便表述，首先区分左侧表达式和右侧表达式
FooL = Foo, FooR = Foo; 
// 下面根据规范逐步推演
O = FooR.prototype = Foo.prototype 
L = FooL.__proto__ = Function.prototype 
// 第一次判断
O != L 
// 循环再次查找 L 是否还有 __proto__ 
L = Function.prototype.__proto__ = Object.prototype 
// 第二次判断
O != L 
// 再次循环查找 L 是否还有 __proto__ 
L = Object.prototype.__proto__ = null 
// 第三次判断
L == null 
// 返回 false
```


```