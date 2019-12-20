---
title: Object原型对象上的方法
categories: 前端
date: 2019-04-24 23:25:28
tags: [JavaScript,前端,编程]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# Object.prototype.hasOwnProperty()

**返回值：** 一个布尔值

**作用：** 可以检测一个属性是存在于实例中，还是存在于原型中。这个方法（不要忘了它是从 Object 继承来的）只在给定属性存在于对象实例中时，才会返回 true 。

**例子：** 

```javascript
function Person(){
}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
    alert(this.name);
};
var person1 = new Person();
var person2 = new Person();
alert(person1.hasOwnProperty("name")); //false
person1.name = "Greg";
alert(person1.name); //"Greg"——来自实例
alert(person1.hasOwnProperty("name")); //true
alert(person2.name); //"Nicholas"——来自原型
alert(person2.hasOwnProperty("name")); //false
delete person1.name;
alert(person1.name); //"Nicholas"——来自原型
alert(person1.hasOwnProperty("name")); //false
```

# Object.prototype.valueOf()

**返回值：** 该指定对象的原始值

> 不同类型对象的valueOf()方法的返回值

| **对象** | **返回值**                                               |
| :------: | -------------------------------------------------------- |
|  Array   | 返回数组对象本身。                                       |
| Boolean  | 布尔值。                                                 |
|   Date   | 存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。 |
| Function | 函数本身。                                               |
|  Number  | 数字值。                                                 |
|  Object  | 对象本身。这是默认情况。                                 |
|  String  | 字符串值。                                               |
|          | Math 和 Error 对象没有 valueOf 方法。                    |

**例子：**

```javascript
//待填充
```

# Object.prototype.toString()

**返回值：** 返回 "[object *type*]"

**例子：**

``` javascript
var obj = {};
obj.toString();//[object Object]
```

**应用：**

## 使用toString()检测对象类型

```javascript
Object.prototype.toString.call(new Array)// [object Array]
Object.prototype.toString.call(new Date)// [object Date]
Object.prototype.toString.call(new String)// [object String]
Object.prototype.toString.call(Math)// [object Math]
//自从 JavaScript 1.8.5 之后
Object.prototype.toString.call(undefined); // [object Undefined]
Object.prototype.toString.call(null); // [object Null]
```



# Object.prototype.toLocaleString()

# Object.prototype.isPrototypeOf()

等




><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>