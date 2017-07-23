---
title: juqery链式调用原理
date: 2017-7-23
tags：链式调用
categories: javaScript
---
aQuery().init().name()

分解：

a = aQuery();
a.init()
a.name()

把代码分解一下，很明显实现链式的基本条件就是要实例对象先创建好，调用自己的方法。

```

aQuery.prototype = {
    init: function() {
        return this;
    },
    name: function() {
        return this
    }
}

```

所以我们如果需要链式的处理，只需要在方法内部返回当前的这个实例对象this就可以了，因为返回当前实例的this，从而又可以访问自己的原型了，这样的就节省代码量，提高代码的效率，代码看起来更优雅。但是这种方法有一个问题是：所有对象的方法返回的都是对象本身，也就是说没有返回值，所以这种方法不一定在任何环境下都适合。

虽然Javascript是无阻塞语言，但是他并不是没阻塞，而是不能阻塞，所以他需要通过事件来驱动，异步来完成一些本需要阻塞进程的操作。