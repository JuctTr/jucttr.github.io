---
title: 七种数据类型和typeof&instanceof
date: 2019-03-17 14:19:14
tags: [编程,JavaScript,Web]
categories: 前端
---

在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# JavaScript的七种数据类型和typeof&instanceof操作符

- ### 七种数据类型
>基本数据类型（简单数据类型或原始类型）：**Undefined、Null、Boolean、Number、String**
>复杂数据类型：**Object**
>ES6新增的数据类型：**Symbol**
>对象是最复杂的数据类型，他可以分为三个子类型：**object、array、function**（不正规说法）
	
- ### typeof操作符

```javascript
	var s = "yicong";
	var b = true;
	var n = null;
	var u;
	var o = new Object();
	function f(){};
	typeof s;//string
	typeof b;//boolean
	typeof n;//object 特殊
	typeof u;//undefined
	typeof o;//object
	typeof f;//function 
	typeof Symbol();//symbol
	typeof {};//object
	typeof [];//object
	typeof window;//object
```
>如上所知：
#### 当在检测引用类型的时候，typeof它返回的结果都是Object，所以在检测引用值类型的时候typeof的用处并不大，所以我们使用了ECMAScript提供的instanceof操作符来检测引用类型值。
- 如果是引用类型值，那么instanceof操作符就会返回**true**；
- **注意：**所有**引用类型**的值都是**Object的实例**，如果使用instanceof操作符去检测基本类型的值，则它会返回**false**；
> ### 为什么所有引用类型的值都是Object的实例？
因为当你在控制台写下 [] 的时候，它已经给你隐式帮你new Array()了，Array()是一个构造函数，所以[]就是对象的实例。
- **解答：**因为基本类型不是对象

## 手撕instanceof操作符

```javascript
	function instance_of(ordinary,construct){
		let conProto = construct.prototype;
		ordinary = ordinary.__proto__;
		while(true){//一直循环下去，也就是在ordinary的原型链上寻找，直到ordinary的原型链上有construct.prototype为止
			if(ordinary === null){
				return false;
			}	
			if (ordinary === conProto){
				return true;
			}
			ordinary = ordinary.__proto__;
		}
	}
```

>**也就是说：**
- ordinary对象是不是construct构造函数构造（new）出来的，
- ordinary对象的原型链上有没有construct的原型


><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>