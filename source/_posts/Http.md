---
title: JavaWeb-Http协议
date: 2018-03-10
tags: [JavaWeb]
categories:
- JavaWeb
- Http协议
keywords: javaweb入门,Http协议
description: Http协议
comments:
password:
copyright: true
---
**请求头**

请求行
多个请求头信息:头名称:头值
空行
请求体

**响应头**

响应行(协议/版本   状态码 状态码的解析)
响应头(key/value格式)
空行
响应正文

**正文**

表单是一大堆内容，而发送给服务器的只有一行字符串



POST请求可以有体，GET请求不能有请求体

Referer: 请求来自哪个页面

Content-Type:application/x-www-form-urlencoded

表单数据类型，说明会使用url格式编码数据；url编码的数据都是以%为前缀，后面跟随两位的16进制

 Content-Length:13:

 请求体的长度

 keyword = hello;

请求体内容



200：请求成功
404：请求的资源没有找到，说明客户端错误的请求了不存在的资源
500：请求资源找到了，但是服务器内部出现了错误
302：重定向，表示服务器要求浏览器重新再发一个请求，服务器会发送一个响应体Location，它指定了新请求的URL地址



**什么是http协议：**

HTTP协议就是一套基于tcp/ip协议的应用层协议
。简单来说，就是一个基于应用层的通信规范，双方要进行通信，大家都要遵守一个规范，这个规范就是HTTP协议。它规定了客户端（通常是浏览器）和服务器之间的通信方式。

**HTTP协议工作原理？**

HTTP协议基于请求响应模型。

一次请求对应一次响应。

首先客户端发送一个请求(request)给服务器，服务器在接收到这个请求后将生成一个响应(response)返回给客户端。

**HTTP协议的特点是什么 ?**

1. 它是一个无状态的协议，服务器端在处理相应请求后不会保留任何客户端的信息，每次请求都是独立的
2. 客户端与服务器端的每一次数据交互，都要经过一次请求/响应的过程。
3. 服务器端无法识别能够出发客户端请求的方法。
4. 一个典型的HTTP请求分为 一个请求行 若干请求头 一个空行 实体内容。

**get和post请求的区别？**

1. get请求用来从服务器上获得资源，而post是用来向服务器提交数据；
2. get将表单中数据按照name=value的形式，添加到action 所指向的URL 后面，并且两者使用"?"连接，而各个变量之间使用"&"连接；post是将表单中的数据放在HTTP协议的请求头或消息体中，传递到action所指向URL；
3. get传输的数据要受到URL长度限制（1024字节）；而post可以传输大量的数据， POST数据是没有限制的，上传文件通常要使用post方式；
4. 使用get时参数会显示在地址栏上，如果这些数据不是敏感数据，那么可以使用get；对于敏感数据还是应用使用post；
5. get使用MIME类型application/x-www-form-urlencoded的URL编码（也叫百分号编码）文本的格式传递参数，保证被传送的参数由遵循规范的文本组成，例如一个空格的编码是"%20"。
6. Jsp页面中的FORM标签里的method属性为get时调用doGet()，为post时调用doPost()

**Http和Https的区别？**

HTTP协议传输的数据都是未加密的，也就是明文的，因此使用HTTP协议传输隐私信息非常不安全，为了保证这些隐私数据能加密传输，于是网景公司设计了SSL（Secure Sockets Layer）协议用于对HTTP协议传输的数据进行加密，从而就诞生了HTTPS。简单来说，HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，要比http协议安全。

推荐博文：

[WEB开发入门](https://www.cnblogs.com/xdp-gacl/p/3729033.html)

[Http协议](https://www.cnblogs.com/xdp-gacl/p/3751277.html)



