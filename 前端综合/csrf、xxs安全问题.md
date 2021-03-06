---
title: CSRF、XSS安全问题
date: 2017-7-24
tags: [前端安全]
categories: 前端综合
---
## XSS：跨站脚本攻击
1. 原因：应用程序在接受数据之后没有进行适当的验证和转义，直接发送给网页浏览器，可能会产生XSS攻击。
2. 危害：恶意的HTML/JavaScript代码会注入到用户浏览的网页上，从而达到Cookie资料窃取、会话劫持、钓鱼欺骗等攻击。
3. 防御方法：
    - HttpOnly 。  浏览器禁止页面的JS访问带有HttpOnly属性的Cookie，从而保证安全。
    -  输入检查 XSS Filter 。    对输入内容做格式检查，类似“白名单”，可以让一些基于特殊字符的攻击失效。
    -  输出检查 。    在变量输出到html页面时，可以使用编码或转义的方式来防御XSS攻击。
    - 对富文本进行处理
    - 防御DOM Based XSS    如果是输出到事件或脚本，要做一次javascriptEncode；如果是输出到HTML内容或者属性，要做一次HtmlEncode。
     
## CSRF：跨站请求伪造，XSS是实现CSRF的其中一种方法。
1. 情景：
    1. 用户在登录受信任网站A后，在本地生成Cookie。
    2. 在不登出A的情况下，访问危险网站B。
    3. 危险网站B中存在访问网站A的链接，当访问网站B后，比如有一个img标签中的一个src指向网站A，则浏览器会带上网站A上的cookie向网站A发送get请求，这样就会产生CSRF攻击，例如银行网站。
2. 原因：XSS是利用用户对当前网站的信任来发起攻击，而CSRF是利用网站对用户的信任来发起攻击。重要操作的所有参数都是可以被攻击者猜测到的。攻击者预测出URL的所有参数与参数值，才能成功地构造一个伪造的请求，将使用用户浏览器向存在漏洞的应用程序发起请求。
3. 防御方法：  
    1. 验证码、  Referer Check 检查请求是否来自合法的源（可被伪造）。
    2. 对于任何重要的请求都需要重新验证用户的身份；
    3. 通用方法：使用Anti-CSRF Token   在URL中保持原参数不变，新增一个参数Token。Token的值是随机的（必须使用足够安全的随机数生成算法，或者采用真随机数生成器），其为用户与服务器所共同持有，可以放在用户的Session中，或者浏览器的Cookie中。 每次session使用同一个Token，开发者就可以自动带上当前页面的token。如果token校验不通过，则证明此次提交并非从本站发送来，则终止提交过程   