### Iterator遍历器
**Iterator 的作用有三个：**
1. 为各种数据结构，提供一个统一的、简便的访问接口；
2. 使得数据结构的成员能够按某种次序排列；
3. ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。

**遍历过程：**

（1）创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。

（2）第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。

（3）第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。

（4）不断调用指针对象的next方法，直到它指向数据结构的结束位置。

每一次调用next都会返回一个包含value和node属性的对象，其中node是boolean类型代表遍历是否结束。

默认的Iterator接口部署在数据结构的Symbol.iterator属性

**调用场合**
1. 解构赋值
2. 扩展运算符
3. yied*
4. for...of
    
    Array.from()
    
    Map(), Set(), WeakMap(), WeakSet()（比如new 
    
    Map([['a',1],['b',2]])）
    
    Promise.all()，Promise.race()

**创建遍历器属性**
```
const obj = {
    [Symbol.iterator] = function(){
        return {
            next:function(){
                return{
                    value:1
                    done:true
                }
            }
        }
    }
}


```

### for...of循环
for...of循环内部调用的是数据结构的Symbol.iterator方法。
1. 数组
>for...of循环调用遍历器接口，数组的遍历器接口==只返回具有数字索引的属性==,当索引不是数字值对应的值不会返回

```
let arr = [3, 5, 7];
arr.foo = 'hello';

for (let i in arr) {
  console.log(i); // "0", "1", "2", "foo"
}

for (let i of arr) {
  console.log(i); //  "3", "5", "7"
}

```
2. Set和Map

```
var engines = new Set(["Gecko", "Trident", "Webkit", "Webkit"]); 
for (var e of engines) 
{ console.log(e); }
// Gecko
// Trident
// Webkit
var es6 = new Map(); 
es6.set("edition", 6); 
es6.set("committee", "TC39"); 
es6.set("standard", "ECMA-262"); 
for (var [name, value] of es6) 
{ console.log(name + ": " + value); }
// edition: 6
// committee: TC39
// standard: ECMA-262
```
遍历的顺序是添加的顺序；set只返回一个值，map返回一个数组，[key,value]
4. 类数组对象，不是所有类数组对象都有Interator接口，可以使用Array.from进行转换
5. for in的缺点，是为遍历对象设计，不适合数组
    
```
数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等等。

for...in循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。

某些情况下，for...in循环会以任意顺序遍历键名。
```
6. for of的优点

```
有着同for...in一样的简洁语法，但是没有for...in那些缺点。

不同于forEach方法，它可以与break、continue和return配合使用。

提供了遍历所有数据结构的统一操作接口。
```
