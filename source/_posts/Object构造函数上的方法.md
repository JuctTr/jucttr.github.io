---
title: Object构造函数上的方法
categories: 前端
date: 2019-04-24 23:23:26
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# 使用for-in循环

>在使用 for-in 循环时，返回的是所有能够通过对象访问的、可枚举的（enumerated）属性，其中既包括存在于**实例**中的属性，也包括存在于**原型**中的属性。屏蔽了原型中不可枚举属性（即将[[Enumerable]] 标记为 false 的属性）的实例属性也会在 for-in 循环中返回。
>
>IE 早期版本的实现中存在一个 bug，即屏蔽不可枚举属性的实例属性不会出现在 for-in 循环中。

**例子：**

```javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.job = "Web前端";
Person.prototype.sayName = function(){
    alert(this.name);
}
var person = new Person();
for(var prop in person){
    console.log(prop);
}
//name
//age
//job---->原型上的属性
//sayName---->原型上的方法
```

ECMAScript 5 也将 constructor 和 prototype 属性的 [[Enumerable]] 特性设置为 false

原生的 constructor 属性是不可枚举的。但我们可以通过Object.defineProperty()来使constructor可枚举。

# Object.defineProperty(obj, prop, descriptor)

- `obj`

  要在其上定义属性的对象。

- `prop`

  要定义或修改的属性的名称。

- `descriptor`

  将被定义或修改的属性描述符。

```javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.job = "Web前端";
Person.prototype.sayName = function(){
    alert(this.name);
}
Object.defineProperty(Person.prototype,'constructor',{
    enumerable: true
})
var person = new Person();
for(var prop in person){
    console.log(prop);
}
//name
//age
//constructor---->原型中的constructor属性
//job---->原型上的属性
//sayName---->原型上的方法
```



# Object.key()

**返回值：** 返回一个包含所有给定对象**自身**可枚举的**实例**属性名称的数组。

```javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}
Person.prototype.job = "Web前端";
Person.prototype.sayName = function(){
    alert(this.name);
}
var canEnum = Object.keys(person);
console.log(canEnum);//["name","age"]---->注意：原型上的属性和方法都不会被返回
```



# Object.getOwnPropertyNames()

**返回值：** 可枚举和不可枚举的**实例属性**的名称被返回

```javascript
var obj ={
    a: 1,
    b: 2
}
Object.prototype.c = 3;//原型上的属性c
Object.defineProperty(obj, 'b',{//b已经被设置为不可枚举的了
    enumerable: false
})

var canEnum = Object.getOwnPropertyNames(obj);
console.log(canEnum);//["a", "b"]可枚举和不可枚举的实例属性都被返回了
```



# Object.create()

# Object.freeze()

# Object.is()



等等等等






><span style="font-size:12px">
>文章标题: <a href="{{permalink}}">{{ title }}</a>
>文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
>许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
>		  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
></span>