---
title: Web浏览器缓存机制
date: 2017-7-08
tags: [浏览器缓存]
categories: 网络
---

##  一、浏览器的缓存规则
>从新鲜度和检验值两个维度来规定浏览器是否直接使用缓存中的副本还是重新获取资源。

### 新鲜度(过期机制，优先级高)
1. Expires(过期日期)
2. Cache-Control(max-age(多少秒数后过期)
3. no-chahe(忽略缓存的副本而向服务器发送请求)
4. no-store(强制缓存不要保留副本并直接向服务器发送请求)

不会发送请求到服务器去验证资源的新旧程度，满足任一即可：

1. 含有完整的过期时间控制头信息（HTTP协议报文），并且仍在有效期内
2. 浏览器已经使用过这个缓存副本，并且在一个会话中已经检查过新鲜度。

    
### 校验值(验证机制)
1. Last-Modified（文件最后修改时间）
2. ETag(文件标识，只要文件改变标识就会变化)(优先级高))第二次请求时会将If-Modified-Since或者If-None-Match发送给服务器验证资源的新旧程度
    
服务器返回资源的时候有时在控制头信息带上这个资源的实体标签Etag（Entity Tag），它可以用来作为浏览器再次请求过程的校
验标识。如过发现校验标识不匹配，说明资源已经被修改或过期，浏览器需要重新获取资源内容。

## 二、浏览器缓存的控制
### 使用HTML Meta标签
    
<META HTTP-EQUIV="Pragma" CONTENT="no-cache">
告诉页面忽略缓存副本，每次都向服务器请求资源，
缓存代理器不支持，部分浏览器不支持

### 使用缓存相关的HTTP消息报头

#### 1.Cahce-Control与Expires

Cache-Control与Expires的作用一致，都是指明当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据。只不过Cache-Control的选择更多，设置更细致，如果同时设置的话，其优先级高于Expires。

#### 2.Last-Modified/ETag与Cache-control/Expries

- 配置Last-Modified/ETag的情况下，浏览器再次访问统一URI的资源，还是会发送请求到服务器询问文件是否已经修改，如果没有，服务器会只发送一个304回给浏览器，告诉浏览器直接从自己本地的缓存取数据；如果修改过那就整个数据重新发给浏览器；

- Cache-Control/Expires则不同，如果检测到本地的缓存还是有效的时间范围内，浏览器直接使用本地副本，不会发送任何请求。两者一起使用时，Cache-Control/Expires的优先级要高于Last-Modified/ETag。即当本地副本根据Cache-Control/Expires发现还在有效期内时，则不会再次发送请求去服务器询问修改时间（Last-Modified）或实体标识（Etag）了。


- 一般情况下，使用Cache-Control/Expires会配合Last-Modified/ETag一起使用，因为即使服务器设置缓存时间, 当用户点击“刷新”按钮时，浏览器会忽略缓存继续向服务器发送请求，这时Last-Modified/ETag将能够很好利用304，从而减少响应开销。

#### 3.Last-Modified与ETag
服务器会优先验证ETag，一致的情况下，才会继续比对Last-Modified你可能会觉得使用Last-Modified已经足以让浏览器知道本地的缓存副本是否足够新，为什么还需要Etag（实体标识）呢？HTTP1.1中Etag的出现主要是为了解决几个Last-Modified比较难解决的问题：

- Last-Modified标注的最后修改只能精确到秒级，如果某些文件在1秒钟以内，被修改多次的话，它将不能准确标注文件的新鲜度

- 如果某些文件会被定期生成，当有时内容并没有任何变化，但Last-Modified却改变了，导致文件没法使用缓存

- 有可能存在服务器没有准确获取文件修改时间，或者与代理服务器时间不一致等情形

## 三、哪些请求不能被缓存
无法被浏览器缓存的请求：
1. HTTP信息头中包含Cache-Control:no-cache，pragma:no-cache，或Cache-Control:max-age=0等告诉浏览器不用缓存的请求
2. 需要根据Cookie，认证信息等决定输入内容的动态请求是不能被缓存的
3. 经过HTTPS安全加密的请求
4. POST请求无法被缓存
5. HTTP响应头中不包含Last-Modified/Etag，也不包含Cache-Control/Expires的请求无法被缓存
