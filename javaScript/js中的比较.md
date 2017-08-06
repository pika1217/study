---
title: js中的比较
date: 2017-8-7
tags: js中的比较
categories: javaScript
---
## ===
1. 在基本类型的比较中===是直接比较数值
2. 在引用类型的数值比较中比较的是地址
```
+0 ==(=) -0  //true
NaN ==(=) NaN  //false
[] ==(=) []  //false
{} ==(=) {}  //false

//Object和===基本相同，只要注意以下几个
Object.is(+0, -0)  //false
Object.is(NaN, NaN)  //true

```

## ==
1. undefined == null，结果是true。且它俩与所有其他值比较的结果都是false。
2. String == Boolean，需要两个操作数同时转为Number。
3. String/Boolean == Number，需要String/Boolean转为Number。
4. Object == Primitive，需要Object转为Primitive(具体通过valueOf和toString方法)。

```

[]==[]  //false
{}=={}  //false
[]==![]  //true
{}==!{}  //false
{}==![]  //VM1896:1 Uncaught SyntaxError: Unexpected token ==
![]=={}  //false
[]==!{}  //true
undefined==null  //true
+0 === -0  //true
NaN == NaN  //false
NaN !== false  //true

```