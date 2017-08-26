## 检测插件
在非ie中，navigator.plugins数组中保存了所有插件信息
，每个插件包含name、description、filename、length等属性。

在非ie中检测插件：

```
function hasPlugin(name){
    name = name.toLowerCase();
    for(var i = 0 ; i < navigator.plugins.length;i++){
        if(navigator.plugiins[i].name.toLowerCase().indexOf(name) > -1){
            return true;
        }
    }
    return false;
}
```

在ie中

```
function hasIePlugin(name){
    try{
        new ActiveObject(name);//name为插件唯一COM标识
        return true;
    }catch(ex){
        return false;
    }
}
```

兼容检测

function hasFlash(){
    var result = hasPlugin("Flash");
    if(!result){
        result = hasIEPlugin("shockwaveFlash.ShockwaveFlash")
    }
    return true;
}

## 注册处理程序

