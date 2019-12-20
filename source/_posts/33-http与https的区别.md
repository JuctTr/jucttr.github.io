---
title: 33.http与https的区别
categories: 网络
date: 2019-09-10 12:24:46
tags: [网络]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# HTTP

http主要的不足之处：

1. 通信使用明文的方式发送内容，不提供任何方式的数据加密，内容可能会被窃听。
2. 不验证通信双方的身份，因此有可能遭遇伪装。
3. 无法证明报文的完整性，所以有可能已经遭篡改。

默认端口：80

# HTTP + 加密 + 认证 + 完整性保护 = HTTPS



​	https 并非 是应用层的一种协议。只是http通信接口部分用`SSL（Secure Socket Layer）`和`TLS（Transport Layer Security ）`协议代替而已。

​	原来的http是直接与TCP通信，而当使用了安全套接层SSL之后，变成了先与SSL通信，再由SSL与TCP通信，简而言之，HTTPS其实就是身披SSL协议外壳的HTTP。



## https采用混合加密机制



### 共享密钥加密

​	**特点：**加密和解密都用同一种密钥。这种方式在通信的时候，是要把密钥同时发送给通信双方。

​	**存在问题：**如何确定是否安全的到达双方，如果密钥在通信过程中被攻击者窃取，那么加密将失去意义？？？



### 公开密钥加密

​	`公开密钥加密`解决了`共享密钥加密`的困难；它采用了一对**非对称**的密钥，一把叫`私有密钥`，另一把叫`公开密钥`。私有密钥不能让其他任何人知道，而公开密钥则可以随意公布，网络上的任何人都可以获得。

**过程：**发送密文的`A方`使用`B方`的**公开密钥**对通信内容进行加密处理，B方收到被加密的信息后，再使用自己的**私有密钥**进行解密，所以在解密的时候不需要像共享密钥解密那样，使用对方发送过来的密钥解密，而是使用自己的私有密钥解密，当然就不必担心密钥被攻击者窃听而被盗走。

​	**存在问题：**无法证明公开密钥本身是是否就是货真价实的公开密钥？假如在公开密钥传输过程中，真正的公开密钥已经被攻击者替换掉了，该怎么解决这个问题？



默认端口：443



### 数字证书认证机构

![](https://o0b5sq.bn.files.1drv.com/y4m1gukCuEwW1oDl8QT8XJCXfhItkCpxjvb0YNBiAqJ4eekUSQp4_Tvq-KhcCuIxdlxLk3yDSlQLvENMPYSn11HahXZA4wMiwBRczDUBa8Czko4JyhCqS0aCl7L-3V928gyV2xgv7ldUkmkfVrL77KUqCseZJqVLMqMjlwoZWeUQPi5KEJrochls8gX44VQJqehUi7z-viIKdqa6GpSPbDFVA?width=3024&height=2568&cropmode=none)



### https存在问题

1. SSL通信通信慢，因为加密和解密都需要进行运算处理，所以从一定的程度上讲，HTTP会更多地消耗服务器和客户端的硬件资源，导致负载增强。
2. 加密通信会消耗跟多的CPU及内存等资源。
3. 购买证书需要开销

**改善：**

- 使用SSL加速器（专用服务器）硬件来改善这个问题。提高数倍SSL的计算速度；分担负载。
- 非敏感信息使用HTTP通信，而涉及到个人信息等敏感数据时，才利用HTTPS加密通信。



## HTTP/1.1——标准化协议

**HTTP/1.1 消除了大量歧义内容并引入了多项改进：**

- 连接可以复用，节省了多次打开TCP连接加载网页文档资源的时间。（持久连接）
- 增加流水线操作，允许在第一个应答被完全发送之前就发送第二个请求，以降低通信延迟。（管线化）
- 支持响应分块。
- 引入额外的缓存控制机制。
- 引入内容协商机制，包括语言，编码，类型等，并允许客户端和服务器之间约定以最合适的内容进行交换。
- 感谢[`Host`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Host)头，能够使不同域名配置在同一个IP地址的服务器上。



# HTTP状态码

## 1XX

1xx 信息性状态码

101 协议升级，主要用于升级到websocket，也可以用于http2

## 2XX

200  OK

204 NotContent 请求成功，没主体（没有资源返回）

206 范围请求，响应报文包含由Content-Range指定范围的实体内容。

## 3XX

301 永久重定向，URI改了，提醒客户端更新标签

302 临时重定向

303 临时重定向、必须用get请求资源

304 没有修改 从客户端未过期的缓存中找

## 4XX

400 bad request 客户端出现错误

 401 http认证（BASIC认证、DIGEEST认证）

403 访问权限forbidden（资源的访问被服务器拒绝）

404 not found

406 无法使用请求的内容特性来响应请求的网页。说白了就是后台的返回结果前台无法解析就报406错误，一般需要修改数据的传输类型比如：text/plain或application/json

## 5XX

500 internal Server Error 服务器执行发生错误，

503 Service Unavailable 服务器超负载或停机维护



> **参考：**<https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP>
>
> <https://juejin.im/entry/5981c5df518825359a2b9476>
>
> 《图解HTTP》


><span style="font-size:12px">
>文章标题: <a href="{{permalink}}">{{ title }}</a>
>文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
>许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
>		  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
></span>