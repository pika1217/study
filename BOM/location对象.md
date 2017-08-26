既是window对象的属性也是document属性
属性名|例子|说明
--|--|--
hash|'#contents'|返回url中的hash
host|'www.wrox.com:80'|服务器名称和端口
hostname|'www.wrox.com'|服务器名称
href|'http://www.wrox.com'|完成的url
path|'/wily/'|url中的目录或文件
port|'8080'|端口或空字符串
protocol|'http'|返回页面使用的协议
search|'?q=javascript'|返回url的查询字段


调用location.replace()方法之后跳转到新的界面并且不能回退

location.reload()//重新加载(可能从缓存中加载)

location.reload(true) //从服务器端请求资源加载