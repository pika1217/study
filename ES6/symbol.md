## 作用
从根本上防止属性名的冲突
1. 相同参数的Symbol函数的返回值不相等

```
// 有参数的情况
var s1 = Symbol('foo');
var s2 = Symbol('foo');
都生成了全局的Symbol类型
s1 === s2 // false
```
2. 不能喝其它类型的值进行运算，可以调用toString()转为字符串
3. 作为属性名的Symbol,不能用点运算符
```
var mySymbol = Symbol();
var a = {
    [mySymbol] : 'hello' //不放[]中就是字符串
}

var a = {}
a[mySymbol] = hello

Object.defineProperty(a,mySymbol,{value:'hello'})

```
    1. 定义一组常量

4. 属性名的遍历
>Symbol 作为属性名，该属性不会出现在for...in、for...of循环中，也不会被Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回。但是，它也不是私有属性，有一个Object.getOwnPropertySymbols方法，可以获取指定对象的所有 Symbol 属性名。

>Reflect.ownKeys 返回所有类型的键名，包括常规键名和 Symbol 键名。

5. Symbol.for和Symbol.keyFor

    Symbol.for搜索有没有以其中参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值。Symbol.for()与Symbol()这两种写法，都会生成新的Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会

    Symbol.keyFor方法返回一个已登记的 Symbol 类型值的key。未登记的Symbol值，返回undefined

**用途** ：单例模式
const FOO_KEY = Symbol('foo');

function A() {
  this.foo = 'hello';
}

if (!global[FOO_KEY]) {
  global[FOO_KEY] = new A();
}

module.exports = global[FOO_KEY];

