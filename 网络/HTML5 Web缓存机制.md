---
title: HTML5 缓存机制
date: 2017-7-08
tags: [HTML5缓存]
categories: HTML
---
#### HTML5 之离线应用Manifest
    
1. 在服务器上添加MIME TYPE支，让服务器能够识别manifest后缀的文件AddType text/cache-manifest  manifest
2. 创建一个后缀名为.manifest的文件，把需要缓存的文件按格式写在里面，并用注释行标注版本

        CACHE MANIFEST
        # 直接缓存的文件
        CACHE:
        Path/to/cache.js
        # version：2012-03-20


3. 给 <html> 标签加 manifest 属性，并引用manifest文件
    <html manifest=”path/to/name-of.manifest”>
    
**离线应用访问及更新流程**：

第一次访问离线应用的入口页HTML（引用了manifest文件），正常发送请求，获取manifest文件并在本地缓存，陆
续拉取manifest中的需要缓存的文件再次访问时，无论在线离线与否，都会直接从缓存中获取入口页HTML和其他缓
存的文件进行展示。如果此时在线，浏览器会发送请求到服务器请求manifest文件，并与第一次访问的副本进行比
对，如果发现版本不一致，会陆续发送请求重新拉取入口文件HTML和需要缓存的文件并更新本地缓存副本。
之后的访问重复第2步的行为

**离线机制的缓存用途**：

从Manifest的机制来看，即使我们不是为了创建离线应用，也同样可以使用这种机制用于缓存文件，可以说是给Web缓存提供多一种可以选择的途径。

**存在的问题**：缓存文件更新控制不灵活
就目前HTML5提供的manifest机制来讲，一个页面只能引用一个manifest页面，而且一旦发现这个manifest改变了，就会把里面所有定义的缓存文件全部重新拉取一遍，不管实际上有没有更新，控制比较不灵活。针对这个问题，也有的同学提出了一些建议，比如把需要缓存的文件分模块切分到不同manifest中，并分开用HTML引用，再使用强大的iframe嵌入到入口页面，这样就当某一个模式需要有更新，不会导致其他模块的文件也重新拉取一遍。

#### HTML5 之本地存储localstorage

HTML5给我们提供本地存储localstorage特性，严格来讲，其实已经不算传统Web缓存的范畴。因为它存储的地方是跟Web缓存分开的，是浏览器重新开辟的一个地方。

##### localstorage的作用

本地存储localstorage的作用主要使Web页面能够通过浏览器提供的set/get接口，存储一些自定义的信息到本地硬盘，并且在单次访问或以后的访问过程中随时获取或修改。

##### Localstorage的使用

Localstorage提供了几个非常易用的Api，setItem/getItem/removeItem/clear

##### Localstorage的缓存用途

Localstorage设计的本意可能是用来存储一些用户操作的个性化设置的文本类型的信息和数据，当我们其实也可能拿来当Web缓存区使用，比如我们可以将Base64格式编码的图片信息，存在localstorage中，再次访问时，直接本地获取后，使用Css3的Data:image的方式直接展现出来。

##### 存在的问题：大小限制

按照目前标准，目前浏览器只给每个独立的域名提供5m的存储空间，当存储超过5m，浏览器就会弹出警告框。