---
title: callee、caller详解
categories: 前端
date: 2019-03-26 17:00:22
tags: [JavaScript,Web,编程]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。


<!--more-->

# arguments对象
>arguments对象不是一个 Array 。它是类似于数组（类数组），但除了 长度之外没有任何数组属性。
例如，它没有 pop 方法、sort方法。但是它可以被转换为一个真正的数组：

```javascript

let args = Array.prototype.slice.call(arguments); 
let args = [].slice.call(arguments);

```
# callee
callee是arguments对象的一个属性、用来指向当前执行的函数。
```javascript

	function foo(){
		console.log(arguments);
	}
	foo();

```
![arguments.callee](https://wx1.sinaimg.cn/mw690/007d7DTvgy1g1gdo7h2lgj30cn07iaa5.jpg)

# caller
arguments.caller 指向调用当前函数的函数。
```javascript

	function foo1(){
		console.log(arguments.callee.caller);
	}
	function foo2(){
		foo1();
	}
	foo1();
	foo2();

```
![arguments.callee.caller](https://wx1.sinaimg.cn/mw690/007d7DTvgy1g1ge9owqrrj30fs030a9y.jpg)


><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>