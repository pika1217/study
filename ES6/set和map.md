## 基本用法
1. Set
    1. 数组去重
    ```
    let arr = Array.from(new Set(target));
    ```
    2. 实例属性和方法
        1. 属性 
        
            Set.prototype.constructor：构造函数，默认就是Set函数。
        
            Set.prototype.size：返回Set实例的成员总数。
        2. 操作方法
            
            add、delete、clear、has
        3. 遍历方法
            keys()、values()、entries()、forEach()，Set数据结构的键值相同
            
            ```
            let set = new Set([1, 2, 3]);
            set.forEach((value, key) => console.log(value * 2) )
            ```
        4. 实习并集，交集，差集
            ```
            let a = new Set([1,2,3]);
            let b = new Set([4,3,2]);
            
            //并集
            let union = new Set([...a,...b]);
            
            //交集
            let intersect = new Set([...a]).filter(x =>b.has(x));
            
            // 差集
            let diff = new Set([...a]).filter(x=>!b.has(x));
            ```
2. WeakSet 不可遍历
    1. weakSet成员只能是对象；
    
    2. WeakSet中的对象都是弱引用，即垃圾回收机制不考虑  对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。
    3. 接收一个数组或类数组作为参数，数组的成员自动成为weakSet的成员，所以数组的成员需要是对象  
    4. 三个方法：delete、has、add
    5. 没有size属性，不能遍历，成员都是弱引用，随时可能消失
    6. 可以用来保存DOM节点，而不用担心这些节点从文档移除而不用担心内存泄露
3. Map
    1. 接受一个数组作为参数，数组成员是一个个键值对的数组
    ```
        const map = new Map([
      ['name', '张三'],
      ['title', 'Author']
    ]);
    
    map.size // 2
    map.has('name') // true
    map.get('name') // "张三"
    map.has('title') // true
    map.get('title') // "Author"
    ```
    2. 如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键
    3. 引用类型时Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题。
    4. 实例属性和方法
    size属性，set，get，has，delete，clear方法
    5. 遍历方法
    Map 结构原生提供三个遍历器生成函数和一个遍历方法。
    ```
    keys()：返回键名的遍历器。
    values()：返回键值的遍历器。
    entries()：返回所有成员的遍历器。
    forEach()：遍历 Map 的所有成员。
    ```
        
    ```
    const map0 = new Map()
      .set(1, 'a')
      .set(2, 'b')
      .set(3, 'c');
    
    const map1 = new Map(
      [...map0].filter(([k, v]) => k < 3)
    );
    // 产生 Map 结构 {1 => 'a', 2 => 'b'}
    
    const map2 = new Map(
      [...map0].map(([k, v]) => [k * 2, '_' + v])
        );
    // 产生 Map 结构 {2 => '_a', 4 => '_b', 6 => '_c'}
    ```
    6. 与其他数据结构转换
        1. Map与数组转换
        
        ```
        const myMap = new Map()
          .set(true, 7)
          .set({foo: 3}, ['abc']);
        [...myMap]
        // [ [ true, 7 ], [ { foo: 3 }, [ 'abc' ] ] ]
        ```
        2. 数组转为Map，将数组传入map的构造函数中
    
        ```
        new Map([
          [true, 7],
          [{foo: 3}, ['abc']]
        ])
        // Map {
        //   true => 7,
        //   Object {foo: 3} => ['abc']
        // }
        ```
        3. Map转为对象，如果所有的key都是字符串就可以转化为对象
                
        ```
        function strMapToObj(strMap) {
          let obj = Object.create(null);
          for (let [k,v] of strMap) {
            obj[k] = v;
          }
          return obj;
        }
        
        const myMap = new Map()
          .set('yes', true)
          .set('no', false);
        strMapToObj(myMap)
        // { yes: true, no: false }
        ```
        4. 对象转map
        
        ```
        function objToStrMap(obj) {
          let strMap = new Map();
          for (let k of Object.keys(obj)) {
            strMap.set(k, obj[k]);
          }
          return strMap;
        }
        
        objToStrMap({yes: true, no: false})
        // Map {"yes" => true, "no" => false}
        ```
        5. Map转JSON
        
        如果键名都是字符，可直接转字符串
        ```
        function strMapToJson(strMap) { 
            return JSON.stringify(strMapToObj(strMap)); 
        } 
        let myMap = new Map().set('yes', true).set('no', false); 
        strMapToJson(myMap)
        // '{"yes":true,"no":false}'
        ```
        如果键名有不是字符串的，则转换为数组JSON
        
        ```
        function mapToArrayJson(map) {
            return JSON.stringify([...map]); 
        } 
        let myMap = new Map().set(true, 7).set({foo: 3}, ['abc']); 
        mapToArrayJson(myMap)
        // '[[true,7],[{"foo":3},["abc"]]]'
        ```
        6. JSON转为Map
        
        所有键名都是字符串的时候
        
        ```
        function jsonToStrMap(jsonStr) 
        { 
            return objToStrMap(JSON.parse(jsonStr)); 
        } 
        jsonToStrMap('{"yes": true, "no": false}')
        // Map {'yes' => true, 'no' => false}
        ```
        
4. WeakMap
    1. 区别
        1. WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。
        2. WeakMap的键名所指向的对象，不计入垃圾回收机制
    2. 不能遍历，不能取键名，没有size属性，不支持clear
    3. 四个方法get()、set()、has()、delete()
    4. 用处，外部引用一删除，内部引用就自动被垃圾回收机制清除
        1. 将DOM节点作为键名
        2. 部署私有属性
    



        
