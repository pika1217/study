Ajax原理 http://www.cnblogs.com/mingmingruyuedlut/archive/2011/10/18/2216553.html
```
开局问：原生xhr怎么写？
答：创建一个xhr对象，readystate onload send open blabla
接着问：怎么处理回调？
答：status等于200且readystate等于4的时候，取responseText
处理。
接下来开启http协议分支任务问：http状态码常见有哪些？
答：200，302，304，404，5xx
问：302是啥？304是啥？什么时候会返回304？你刚刚说浏览器缓存，具体缓存机制是怎么样的？
答：…
问：你刚刚说的是发起一个get请求，除此之外httpmethod还有哪些？
答：常用的还有post，put，delete等。问：post跟get有啥区别？答：…http分
支聊得差不多啦，回主线，进入跨域和web前端安全分支。
问：http聊的差不多啦，我们回到xhr，你知道同源策略么？
答：同协议，同端口，同域名
问：怎么跨域发起请求答：cors，jsonp等
接下来聊聊，cors的细节，jsonp的原理。
再接下来聊聊其他跨域的方案，postmessage，document.domain降域接下来就着同源策略，跟面试者聊聊cookie，问题往csrf上走，csrf是啥，怎么
防。顺着csrf，聊聊xss，概念，怎么防？
```
### 原生js创建Ajax
```
function createXHR(){
    if(typeof XMLHttpRequest != "undefined"){  //非IE的版本
        return new XMLHttpRequest();
    }else if(typeof ActiveObject !="undefined"){ //IE的版本
       return new ActiveXObject('Microsoft.XMLHTTP');
    }else{
        throw new Error("系统或浏览器不支持XHR对象!");
    } 
}
// 转义字符
function params(data){
    var arr = [];
    for(var i in data){
        arr.push(encodeURIComponent(i) + "=" + encodeURIComponent(data[i]));
        //get方法必须用encodeURIComponent进行编码
    }
    return arr.join("&");
}

//封装Ajax
function createAjax(obj){
    var xhr = createXHR();//1. 创建一个异步调用对象
    obj.url = obj.url+"?rand=" + Math.random();//清除缓存
    obj.data = params(obj.data);
    if(obj.method === "get"){
        obj.url +=obj.url.indexOf("?") == -1 ?"?"+obj.data : "&" + obj.data;
    }
     /*异步的时候需要随时监听readyState值得变化
    0：未初始化，没调用open函数
    1：启动，调用open()但没调用send()
    2：发送，已经调用send()但没有接收到响应
    3：接收，接收到部分响应数据
    4：完成，接收到全部的响应数据
    */
    if(obj.async === true){
   //异步时必须在open()之前指定onreadystatechange事件处理程序才能保证跨浏览器兼容性
   //2. 将对象状态与事件相关联
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){
                callBack();
            }
        }
    }
    //3. 加载数据所在的服务器页
    xhr.open(obj.method,obj.url,obj.async);
    if(obj.method === "post"){
        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        xhr.send(obj.data);//如果是表单提交请求，可以使用FormData对象对数据进行序列化，即xhr.send(new FormData($("#form_id")))
        // 4. 发送请求
    }else{
        xhr.send(null);
    }
    xhr.abort();//取消异步请求
    if(obj.async === false){
        callBack();
    }
    function callBack(){
        if((xhr.status >=200 && xhr.status < 300) || xhr.status == 304){
        //5. 处理数据
            obj.success(xhr.responseText);
        }else{
            obj.Error("错误代号为："+xhr.status+"错误信息为："+xhr.statusText);
        }
    }
}
createAjax({
    "method " : "post",
    "url" : "func.php",
    "data" :{
        "id":id
    },
    "async" : false,
    "success" : function(data){
        alert(data);
    },
    "Error":function(data){
        alert(data);
    }
})
```
####  过程
    
    (1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.
    (2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.
    (3)设置响应HTTP请求状态变化的函数.
    (4)发送HTTP请求.
    (5)获取异步调用返回的数据.
    (6)使用JavaScript和DOM实现局部刷新.

#### 优缺点
##### 优点：
1. 通过异步模式，提升了用户体验
2. 优化了浏览器和服务器之间的传输，减少不必要的数据往返，减少了带宽占用
3. Ajax在客户端运行，承担了一部分本来由服务器承担的工作，减少了大用户量下的服务器负载

##### 缺点：
1. ajax不支持浏览器back按钮。
2. 安全问题 AJAX暴露了与服务器交互的细节。
3. 对搜索引擎的支持比较弱。
4. 破坏了程序的异常机制。
5. 不容易调试。
6. 不能很好的支持移动设备。


### http请求和ajax请求的区别
1. 
AJAX通xmlHttpRequest象请求服务器服务器接受请求返数据实现刷新交互

普通http请求通httpRequest对象请求服务器接受请求返数据需要页面刷新

2. 
HTTP请求发出者是一个页面，发出的页面同时会处于不可用状态，等待数据刷新。

Ajax中的异步请求发出者是页面中的一个HttpRequest对象，页面本身的显示和操作在请求和接收数据的过程中不受影响。