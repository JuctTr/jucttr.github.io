---
title: 26.XSS攻击和CSRF攻击的防范措施
categories: 前端
date: 2019-09-06 16:51:40
tags: [网络,web安全]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

[TOC]



# XSS攻击

## 一、概述

跨站脚本攻击（Cross-site scripting)是一种Web安全漏洞，是指恶意攻击者在网站的web页面注入恶意的客户端代码。



XSS攻击可以分为3类：反射型（非持久型）、存储型（持久型）、基于DOM。

## 二、种类

### 	2.1    反射型（非持久型）

一般分为这几种情况：

1. 攻击者诱使用户去点击（访问）一个包含有恶意脚本代码的URL（链接），当受害者去点击这个链接时，提交给服务端。服务端返回的内容，也带上了这段XSS代码。最后这段恶意代码就会在受害者主机上的浏览器执行。

   > 举个例子：比如在用户访问的页面上，有一个攻击者恶意链接为`http://loaclhost:8080?q=111&p=222`

2.  

3.   

   

### 	2.2    存储型（持久型）

​	存储型区别于反射型的是，提交的具有攻击性的XSS代码回存储在服务器端；这个一般出现在Form表单、评论留言区、论坛文章等。

> **举一个场景：**
>
> ​	比如我，在一个论坛或者博客上，以一名普通用户的身份，在个性签名或者评论留言区，把个性签名或者在留言区写一段具有攻击性代码`<script>alert(document.cookie)<script>`，这段代码就会按照正常的提交方式，进入数据库持久保存；
>
> ​	若网站没有对用户的输入数据进行过滤，当其他用户（查看这篇文章的时候）浏览这篇文章 or 个人主页时，浏览器（前台）就会获取后端从数据库中读出的注入（攻击性）代码，这时就会在前端渲染执行。
>
> ​	那么最后导致的结果就是：所有访问你个人主页或文章时，都会中招。

攻击成功的条件：

1. 提交表单发起POST请求时，后端没有对用户输入数据进行转义处理
2. 后端从数据库中取出数据没做转义，直接返回给前端页面
3. 前端页面拿到后端数据没做转义直接渲染成DOM

### 	2.3    基于DOM

这个类型的攻击，不需要服务端参与，只发生在客户端的攻击



## 三、防御措施

1. 设置HttpOnly

   

2. 输入输出检查（过滤转义输入输出）

   

3. CSP

# CSRF攻击

## 一、概述

跨站请求伪造（Cross Site Request Forgery），是攻击者借助受害者的 Cookie 骗取服务器的信任，可以在受害者毫不知情的情况下以受害者名义伪造请求发送给受攻击服务器，从而在并未授权的情况下执行在权限保护之下的操作。



现在防止跨站请求伪造的方法是银行在自己的页面里嵌入一个随机数，用户正常访问时连同这个随机数一起提交，而伪造的请求得不到这个随机数，因此银行就不响应它。



>**参考：**<https://github.com/dwqs/blog/issues/68>
>
><https://mp.weixin.qq.com/s?__biz=MzU0OTExNzYwNg==&mid=2247483770&idx=1&sn=4f2247fdf7e1de9d8c45539c09751ba4&chksm=fbb58ab3ccc203a50abf225bdf6db56d10f5b0030cb9f333b245ebb95f8c440673901f7d6c23#rd>
>
><https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%AB%99%E8%AF%B7%E6%B1%82%E4%BC%AA%E9%80%A0>








><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>