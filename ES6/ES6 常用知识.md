---
title: 'ES6 常用知识'
date: 2017-9-2
tags: ES6
categories: ES6
---
###  let 、 const
1. 不能重复定义相同变量名
2. 暂存性死区
3. 没有变量提升
4. 不能在初始化之前使用变量
4. const基本类型变量不可改变值，引用类型不可改变地址
### 模板字符串

第一个用途，基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定。

```
//es5 
    var name = 'lux'
    console.log('hello' + name)
    //es6
    const name = 'lux'
    console.log(`hello ${name}`) //hello lux
```


第二个用途，在ES5时我们通过反斜杠(\)来做多行字符串或者字符串一行行拼接。ES6反引号(``)直接搞定。

```
// es5
    var msg = "Hi \
    man!
    "
    // es6
    const template = `<div>
        <span>hello world</span>
    </div>`
```


对于字符串es6当然也提供了很多厉害的方法。说几个常用的。

```
// 1.includes：判断是否包含然后直接返回布尔值
    let str = 'hahay'
    console.log(str.includes('y')) // true
    // 2.repeat: 获取字符串重复n次
    let s = 'he'
    console.log(s.repeat(3)) // 'hehehe'
    //如果你带入小数, Math.floor(num) 来处理
```

###  箭头函数
1. 不需要function关键字来创建函数
2. 单行可以省略return
3. 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。需要注意的是es6默认严格模式，所以函数中this不能等于window，如果没有指定函数中的this指向，则this等于undefined
4. 箭头函数可以替换函数表达式，但是不能替换函数声明

### 拓展的对象功能

对象初始化简写

ES5我们对于对象都是以键值对的形式书写，是有可能出现键值对重名的。例如：

```
function people(name, age) {
        return {
            name: name,
            age: age
        };
    }
```

键值对重名，ES6可以简写如下：

```
function people(name, age) {
        return {
            name,
            age
        };
    }
```

ES6 同样改进了为对象字面量方法赋值的语法。ES5为对象添加方法：

```
const people = {
        name: 'lux',
        getName: function() {
            console.log(this.name)
        }
    }
```

ES6通过省略冒号与 function 关键字，将这个语法变得更简洁

```
const people = {
        name: 'lux',
        getName () {
            console.log(this.name)
        }
    }
```

ES6 对象提供了Object.assign()这个方法来实现浅复制。Object.assign()可以把任意多个源对象自身可枚举的属性拷贝给目标对象，然后返回目标对象。第一参数即为目标对象。在实际项目中，我们为了不改变源对象。一般会把目标对象传为{}

```
const obj = Object.assign({}, objA, objB)
```
### 赋值解构

```
//对象 
const people = { name: 'lux', age: 20 } 
const { name, age } = people 
console.log(`${name} --- ${age}`) //数组 
const color = ['red', 'blue']
const [first, second] = color console.log(first) //'red' console.log(second) //'blue'

```

### 扩展运算符...

```
//数组
const color = ['red', 'yellow'] 
const colorful = [...color, 'green', 'pink'] 
console.log(colorful) //[red, yellow, green, pink] 

//对象 
const alp = { fist: 'a', second: 'b'} 
const alphabets = { ...alp, third: 'c' } 
console.log(alphabets) //{ "fist": "a", "second": "b", "third": "c" }

```
有时候我们想获取数组或者对象除了前几项或者除了某几项的其他项

```
//数组
const number = [1,2,3,4,5]
const [first, ...rest] = number
console.log(rest) //2,3,4,5
//对象
const user = {
    username: 'lux',
    gender: 'female',
    age: 19,
    address: 'peking'
}
const { username, ...rest } = user
console.log(rest) 
//{"address": "peking", "age": 19, "gender": "female"}
```

### 函数
1. 默认参数
1. class

```

class Person {
  constructor(name, age) {  // 构造函数
    this.name = name;
    this.age = age;
  }
  
  getName() {   // 这种写法表示将方法添加到原型中
    return this.name
  }
  
  static a = 20;  // 等同于 Person.a = 20
  
  c = 20;   // 表示在构造函数中添加属性 在构造函数中等同于 this.c = 20
  
// 箭头函数的写法表示在构造函数中添加方法，在构造函数中等同于this.getAge = function() {}
  getAge = () => this.age   

}

```
3. extends
相比ES5，ES6的继承就要简单很多，我们直接来看一个例子。

```
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  getName() {
    return this.name
  }
}

// Student类继承Person类
class Student extends Person {
  constructor(name, age, gender, classes) {
    super(name, age);//调用父类构造函数返回this指向Student
    this.gender = gender;
    this.classes = classes;
  }
  
  getGender() {
    return this.gender;
  }
}
```
在继承的构造函数中，我们必须如上面的例子那么调用一次super方法，它表示构造函数的继承，与ES5中利用call/apply继承构造函数是一样的功能。

```
// 构造函数中
// es6 
super(name, age);

// es5
Person.call(this);
```
### import 和 export

import导入模块、export导出模块

```
import people from './example' //全部导入
```


```
//有一种特殊情况，即允许你将整个模块当作单一对象进行导入
//该模块的所有导出都会作为对象的属性存在
import * as example from "./example.js"
console.log(example.name)
console.log(example.age)
console.log(example.getName())

//导入部分

import {name, age} from './example'

// 导出默认, 有且只有一个默认

export default App

// 部分导出
export class App extend Component {};
```
1. 当用export default people导出时，就用 import people 导入（不带大括号） 
2. 一个文件里，有且只能有一个export default。但可以有多个export。 
3. 当用export name 时，就用import { name }导入（记得带上大括号） 
4. 当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age } 
5. 当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example

### Promise

>在promise之前代码过多的回调或者嵌套，可读性差、耦合度高、扩展性低。通过Promise机制，扁平化的代码结构，大大提高了代码可读性；用同步编程的方式来编写异步代码，保存线性的代码逻辑，极大的降低了代码耦合性而提高了程序的可扩展性。

发起异步请求

```
fetch('/api/todos')
  .then(res => res.json())
  .then(data => ({ data }))
  .catch(err => ({ err }));

var fn = function(num) {
    return new Promise(function(resolve, reject) {
        if (typeof num == 'number') {
            resolve(num);
        } else {
            reject('TypeError');
        }
    })
}

fn(2).then(function(num) {
    console.log('first: ' + num);
    return num + 1;
})
.then(function(num) {
    console.log('second: ' + num);
    return num + 1;
})
.then(function(num) {
    console.log('third: ' + num);
    return num + 1;
});

// 输出结果
first: 2
second: 3
third: 4

```
### Generators

生成器（ generator）是能返回一个迭代器的函数。生成器函数也是一种函数，最直观的表现就是比普通的function多了个星号*，在其函数体内可以使用yield关键字,有意思的是函数会在每个yield后暂停。

当你调用一个generator时，它将返回一个迭代器对象。这个迭代器对象拥有一个叫做next的方法来帮助你重启generator函数并得到下一个值。next方法不仅返回值，它返回的对象具有两个属性：done和value。value是你获得的值，done用来表明你的generator是否已经停止提供值。

```
// 生成器
function *createIterator() {
    yield 1;
    yield 2;
    yield 3;
}

// 生成器能像正规函数那样被调用，但会返回一个迭代器
let iterator = createIterator();

console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
```

那生成器和迭代器又有什么用处呢？

围绕着生成器的许多兴奋点都与异步编程直接相关。异步调用对于我们来说是很困难的事，我们的函数并不会等待异步调用完再执行，你可能会想到用回调函数，（当然还有其他方案比如Promise比如Async/await）。

生成器可以让我们的代码进行等待。就不用嵌套的回调函数。使用generator可以确保当异步调用在我们的generator函数运行下行代码之前完成时暂停函数的执行。

那么问题来了，咱们也不能手动一直调用next()方法，你需要一个能够调用生成器并启动迭代器的方法。就像这样子的

```
function run(taskDef) { //taskDef即一个生成器函数

    // 创建迭代器，让它在别处可用
    let task = taskDef();

    // 启动任务
    let result = task.next();

    // 递归使用函数来保持对 next() 的调用
    function step() {

        // 如果还有更多要做的
        if (!result.done) {
            result = task.next();
            step();
        }
    }

    // 开始处理过程
    step();

}
```

生成器与迭代器最有趣、最令人激动的方面，或许就是可创建外观清晰的异步操作代码。你不必到处使用回调函数，而是可以建立貌似同步的代码，但实际上却使用 yield 来等待异步操作结束。

参考：
1. http://www.jianshu.com/p/287e0bb867ae
2. http://www.jianshu.com/p/cfb0893c34f1

