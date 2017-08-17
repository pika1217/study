---
title: 'var、let、const区别'
date: 2017-8-9
tags: ES6
categories: ES6
---
ES6新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。
## var和let
### 声明后未赋值，表现相同

```
        var varTest;
        let letTest;
        console.log(varTest); //输出undefined
        console.log(letTest); //输出undefined
```
### 使用未声明的变量，表现不同

```
  console.log(varTest); //输出undefined(注意要注释掉下面一行才能运行)
  console.log(letTest); //直接报错：ReferenceError: letTest is not defined

  var varTest = 'test var OK.';
  let letTest = 'test let OK.';
```
### 重复声明同一个变量

```
        var varTest = 'test var OK.';
        let letTest = 'test let OK.';
        
        var varTest = 'varTest changed.';
        let letTest = 'letTest changed.'; //直接报错：SyntaxError: Identifier 'letTest' has already been declared
        
        console.log(varTest); //输出varTest changed.(注意要注释掉上面letTest变量的重复声明才能运行)
        console.log(letTest);
```

### 变量作用范围，表现不同

```
var varTest = 'test var OK.';
  let letTest = 'test let OK.';

  {
    var varTest = 'varTest changed.';
    let letTest = 'letTest changed.';
  }

  console.log(varTest); //输出"varTest changed."，内部"{}"中声明的varTest变量覆盖外部的letTest声明
  console.log(letTest); //输出"test let OK."，内部"{}"中声明的letTest和外部的letTest不是同一个变量
```
### 总结
1. 使用声明后未赋值的变量，表现相同，都是undefined
2. 使用变量在声明变量之前，表现不同，var会输出undefined，let会直接报错
3. 重复声明初始化一个变量，表现不同，var会输出后面的值，let会直接报错
4. 变量作用范围不同，let有块级作用域，var没有

## let与const

### 相同点
1、块局作用域；
2、不存在变量提升，一定声明后才能使用；
3、暂时性死区，在代码块内使用let命令声明变量之前，该变量都是不可用的，不受外部变量影响；
4、在相同作用域范围内不允许重复声明；

### 不同点
1、const如果声明的变量是简单的值，则不能改变变量的值，修改会报错；
2、const如果声明的是复合类型的变量，则只保证变量地址不变，值可以变；