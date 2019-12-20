---
title: 39.JavaScript继承
categories: 前端
date: 2019-09-28 10:29:24
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

> **前言：**继承的具体概念我就不讲了，很简单，就是爸爸有的特性（年龄、身高等），儿子也有，而儿子在长大的过程中，通过锻炼，可以形成一些爸爸没有的特性（跳舞、弹钢琴等），两者形成了父子关系，又可以有自己独立的特性，起到相辅相成的作用；

<!--more-->

# JavaScript继承

## 种类：

1. 传统原型链继承
2. 借用构造函数继承
3. 组合继承
4. 寄生组合式继承
5. 循环拷贝继承
6. JavaScript多继承



## 传统原型链继承

```javascript
function Father(name, age) {
    this.name = name;
    this.age = age;
    this.money = [1000];
    this.sayInfo = function() {
        console.log('我的名字：' + this.name + '，年龄是：' + this.age);
    }
}
Father.prototype.makeMoney = function (money) {
    this.money.push(money);
}
function Son(name, age) {
    this.name = name;
    this.age = age;
}
Son.prototype = new Father('爸爸', '45'); // Son的原型对象实际上变成了Father构造函数的实例
var son1 = new Son('大儿子', 18);
son1.sayInfo(); 					// 访问Father中的方法sayInfo
son1.makeMoney(90); 				// 访问Father的原型对象中的方法 
var son2 = new Son('二儿子', 16);
console.log(son2.moeny);              // [1000, 90];
```



这种继承的本质就是重写子类（Son）的原型对象，原来存在于Father的实例中的所有方法和属性，现在也存在于Son.prototype中了

### 优点：

​	父类（Father）中的属性和方法以及Father原型上的属性和方法，子类（Son）都可以访问得到。

### 缺点：

- 原型对象（Son.prototype）上的引用类型值，会被所有实例共享。（例如上面的moeny，我们在上面的son1去push一个90，在下面使用son2.money输出[1000, 90]，而不是[1000]）

- 不能同时继承多个父类

-  在创建子类的实例时，不能向父类的构造函数中传递函数。

  

## 借用构造函数继承

```javascript
Father.prototype.makeMoney = function (money) {
    this.money.push(money);
}
function Father(name, age) {
    this.name = name;
    this.age = age;
    this.money = [1000];
    this.sayInfo = function() {
        console.log('我的名字：' + this.name + '，年龄是：' + this.age);
    }
}
function Son(name, age) {
    Father.call(this, name, age);
    this.sex = '男';
}

var son1 = new Son('大儿子', 18);
son1.makeMoney(20); 				// Uncaught TypeError: son1.makeMoney is not a function
son1.money.push(20);
console.log(son1.money); 			// [1000, 20]
var son2 = new Son('二儿子', 16);
console.log(son2.money);			// [1000]

console.log(son1 instanceof Son); 		// true
console.log(son1 instanceof Father); 	// false 
```

### 优点：

- 解决了传统原型链继承中共享引用类型属性的问题；
- 可以继承多个父类；
- 创建子类实例（son1、son2）的时候可以向父级传递参数；

### 缺点：

- 只能继承父类（Father）构造函数里面的属性和方法，不会继承父类原型（Father.prototype）上的属性方法；也就是说在父类原型对象中定义的方法，对子类而言是不可见的。

- 实例只是子类的实例不是父类的实例。

- 方法都在构造函数中定义，因此无法实现**函数复用**（就是每个子类都有父类实例的副本，比如上面的sayInfo方法，son1和son2都有各自的sayInfo，不是同一个，无法实现复用）

  

## 组合继承

​	通过调用父类的构造函数，继承父类构造函数内的属性方法，然后通过将父类实例作为子类原型继承父类原型上的属性和方法，实现函数复用

```javascript
Father.prototype.makeMoney = function (money) {
    this.money.push(money);
}
function Father(name, age) {
    this.name = name;
    this.age = age;
    this.money = [1000];
    this.sayInfo = function() {
        console.log('我的名字：' + this.name + '，年龄是：' + this.age);
    }
}
function Son(name, age) {
    Father.call(this, name, age);			// 第二次调用父类构造函数
    this.sex = '男';
}
Son.prototype = new Father('爸爸', 45);		// 父类实例作为子类原型对象 ; 第一次调用父类构造函数
Son.prototype.constructor = Son;

var son1 = new Son('大儿子', 18);
son1.makeMoney(90);
console.log(son1.money);					// [1000, 90]
var son2 = new Son('二儿子', 16);
console.log(son2.money);					// [1000]

console.log(son1 instanceof Son); 			// true
console.log(son1 instanceof Father); 		// true 
```

### 优点：

- 实现函数复用
- 可以继承多个父类；
- 可以继承父类构造函数里面属性和方法，又可以继承父类原型属性和方法；
- 修改子类的引用类型值，不会影响父类（因为是父类实例作为子类原型对象）

### 缺点：

- 调用了两次父类的构造函数，产生了两份父类实例，多消耗了一点内存。



## 寄生组合式继承 / 圣杯模式继承

```javascript
Father.prototype.lastName = "yicong";
function Father(name,age) {
    this.name = name;
    this.age = age;
}
function Son(name,age) {
    Father.call(this,name,age);				// 把当前函数的this绑到Father
}
// Son.prototype = Object.create(Father.prototype);
// Son.prototype.constructor = Son;
//上面这两行相当于下面的inherit函数
function inherit(Target, Origin) {
    function F() {}; 						// 借助一个F函数
    F.prototype = Origin.prototype; 		// 创建父类“原型”的一个副本
    Target.prototype = new F(); 		// 把父类“原型”的副本实例赋给子类Target的原型
    Target.prototype.constuctor = Target; // 把子类的原型的constuctor属性指向子类自己
    Target.prototype.uber = Origin.prototype;
}
inherit(Son, Father);
Son.prototype.sex = "male";
var son = new Son();
var father = new Father();
// 这样father中就没有了sex属性了
```

### **缺点：**	

- 不能实现多继承。



## 循环拷贝继承



```javascript
Father.prototype.makeMoney = function (money) {
    this.money.push(money);
}
function Father(name, age) {
    this.name = name;
    this.age = age;
    this.money = [1000];
    this.sayInfo = function() {
        console.log('我的名字：' + this.name + '，年龄是：' + this.age);
    }
}
function Son(name, age) {
    var f = new Father(name, age);
    for(var prop in f) {
        Son.prototype[prop] = f[prop];
    }
}
var son1 = new Son('大儿子', 18);
console.log(son1);
console.log(son1 instanceof Son); 			// true
console.log(son1 instanceof Father); 		// false 毕竟只是拷贝
```

![循环拷贝继承](https://987amg.bn.files.1drv.com/y4mfB6rtyV02TihHDNXDu0Bjuz-HjULfF2klqufN8ab-93P_uuseTBRsVZelUcr4_Ofk-bCghtDc3wLs2T0a5OLj9DR5MuzjeVB9-r0KVATtIrZr2RD_ys7qu054MJT6eW0ba3J7k8lJ9eB3iEpGjxSAmBUOa5Ls9Nyd2twQF2xNwbAghvJD2SVxUTNO86Vc9Cj1ENGiakk4Lmly0gk6_IBag?width=532&height=224&cropmode=none)

### 优点：

- 可以继承多个父类；
- 可以将父类的所有属性和方法（包括原型对象，当然前提是可枚举）均继承下来；

### 缺点：

- 效率较低；
- 实例不属于父类的实例。



## JavaScript多继承

```javascript
Father.prototype.makeMoney = function (money) {
    this.money.push(money);
}
function Father(name, age) {
    this.name = name;
    this.age = age;
    this.money = [1000];
    this.sayInfo = function() {
        console.log('我的名字：' + this.name + '，年龄是：' + this.age);
    }
}
function Mather() {
    this.makeFood = function() {
        console.log('我可以下厨');
    }
}
function Son(name, age) {
    Father.call(this, name, age);
    Mather.call(this);
}
for (prop in Father.prototype) {
    Son.prototype[prop] = Father.prototype[prop];
}
for (prop in Mather.prototype) {
    Son.prototype[prop] = Mather.prototype[prop];
}		
var son1 = new Son('大儿子', 18);
console.log(son1);

console.log(son1 instanceof Son); 			// true
console.log(son1 instanceof Father); 		// false 毕竟只是拷贝
console.log(son1 instanceof Mather);		// false 毕竟只是拷贝
```

```javascript
        // 父类A
        function A(x) {
            this.x = x;
        }
        A.prototype.outputA = function () {
            console.log(this.x, this.y, this.z);
        }
        A.prototype.firstName = 'wang';
        // 父类B
        function B(y) {
            this.y = y;
        }
        B.prototype.outputB = function () {
            console.log(this.x, this.y, this.z)
        }
        B.prototype.lastName = 'yicong';
        // 子类，同时继承A和B		
        function Child(x, y, z) {
            A.call(this, x); // 借用构造函数
            B.call(this, y);
            this.z = z;
        }
        Child.prototype = Object.create(A.prototype);
        Child.prototype.constructor = Child;

        (function mixinB() {
            var keys = Object.keys(B.prototype);
            var i, len;
            for (var i = 0, len = keys.length; i < len; i++) {
                Child.prototype[keys[i]] = B.prototype[keys[i]]; // 拷贝
            }
        })();
        Child.prototype.outputChild = function () {
            console.log("子类原型属性")
        }
        var space = new Child(1, 2, 3);
        space.outputA()//1 2 3
        space.outputB()//1 2 3
        console.log(space instanceof Child);//true
        console.log(space instanceof A);//true
        console.log(space instanceof B);//false
```



> **参考：**
>
> <https://mp.weixin.qq.com/s/V6F8vRYwKFOrkxhEkg7peA>
>
> <https://github.com/youngwind/blog/issues/97>
>
> <https://juejin.im/post/5a96d78ef265da4e9311b4d8#heading-0>



><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>