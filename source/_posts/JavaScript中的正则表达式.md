---
title: JavaScript中的正则表达式
categories: 前端
date: 2019-04-04 22:31:56
tags: [JavaScript,Web]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# JavaScript中的正则表达式

## 模式以及支持标志

 ` var expression = / pattern / flags; `
` var 表达式 = / 模式 / 标志;`

 >正则表达式的匹配模式支持下列3个标志。

| 修饰符     |    描述  |
| :--------: | :--------:|
| g（global） | 全局匹配，应用所有字符串，而非在发现第一个匹配后停止 |
| i（ignoreCase）    |   不区分大小写，匹配时忽略模式与字符串的大小写 |
| m（multiline）      |  多行匹配，到达一行文本末尾，继续查找下一行 |

## 两种创建方式
### 字面量定义和构造函数定义
```javascript
	var expression = /[bc]at/i;//字面量定义
	var expression = new RegExp("[bc]at","i");//构造函数定义
```
>RegExp构造函数接收两个参数：**RegExp("要匹配的字符串模式","可选的标志字符串")**
> **注意：** 传递给RegExp构造函数的两个参数必须都是字符串
### 区别：
>由于 RegExp 构造函数的模式参数是字符串，所以在某些情况下要对字符进行**双重转义**。

| 字面量模式     |    构造函数模式  | 
| :-----------:| :------------:| 
![字面量和构造函数的区别](https://wx4.sinaimg.cn/mw690/007d7DTvgy1g1rlmyacdaj30ni05qaab.jpg)

## RegExp实例方法
### test()
### exec()
>exec() 接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组；在没有匹配项的情况下返回 null 。返回的数组虽然是 Array 的实例，但包含两个额外的属性： index 和 input 。
>-  index 表示匹配项在字符串中的位置。
>- input 表示应用正则表达式的字符串。

### match()
> **match()**方法可以以类似数组的形式返回**第一个**与表达式匹配的字符

例子：
```javascript
	var reg = /ab/;
    var str = "abababababab";
   	console.log(str.match(reg));
```
![match()方法](https://wx1.sinaimg.cn/mw690/007d7DTvgy1g1rkxnd2dfj307903o0sk.jpg)
```javascript
	var reg = /ab/g;
    var str = "abababababab";
   	console.log(str.match(reg));
```
![match()全局匹配](https://wx1.sinaimg.cn/mw690/007d7DTvgy1g1rl1300aaj30bq053t8k.jpg)

## 方括号
1. [........]，查找方括号中的任意字符
>比如：
[abc]、[0-9]、[a-z]、[A-Z]、[A-z]、[adgk]
2. [ ^......]，查找方括号中**以外**的任意字符，**^**表示**非**，注意这个**^**是要在[]里面的才表示**非**
>比如：
[^abc]、[^adpk]

3. (......|......|......) ，查找圆括号里面中的指定的其中一个，**|**表示**或**
>比如：
(abc|bcd|def)

## 元字符

|    字符    |    等价类  | 含义 |
| :--------: | :--------:|:-------:|
| **.** | [^\r\n] | 除了回车符和换行符之外的所有字符 |
| \d | [0-9] | 数字字符 |
| \D  | [^0-9] | 非数字字符 |
| \s  | [\t\n\x0B\f\r] | 空白字符 |
| \S  | [^\t\n\x0B\f\r] | 非空白字符 |
| \w  | [a-zA-Z_0-9] | 单词字符（字母、数字下划线） |
| \W  | [^a-zA-Z_0-9] | 非单词字符 |

## 定位符

|    字符  | 含义 |
| :--------: | :--------:|
| ^ | 匹配字符串的开头 |
| $ | 匹配字符串的结尾 |
| \b | 匹配一个单词的边界 |
| \B | 与\b相反，匹配一个非单词边界 |

**用例：**
![\b边界符\B](https://wx4.sinaimg.cn/mw690/007d7DTvgy1g1rvannzymj30a60d1n3c.jpg)

## 量词
|    字符  | 含义 |
| :--------: | :--------:|
| n+ | 匹配任何包含至少一个 n 的字符串 |
| n* | 匹配任何包含零个或多个 n 的字符串 |
| n? | 匹配任何包含零个或一个 n 的字符串 |
| n{x} | 匹配包含 x 个 n 的序列的字符串 |
| n{x,y} | 匹配包含 x 至 y 个 n 的序列的字符串 |
| n{x,} | 匹配包含至少 x 个 n 的序列的字符串 |
| ?=n | 匹配任何其后紧接指定字符串 n 的字符串 |
| ?!n | 匹配任何其后没有紧接指定字符串 n 的字符串 |

## html特殊字符：

![html特殊字符](https://uploadfiles.nowcoder.com/images/20180826/2835751_1535273372355_77416C8562139159984E0DDDE16AD5F8)

## 练习题
1. 将the-first-name转换成theFirstName?
```javascript
        var reg = /-(\w)/g;
        var str = "the-first-name";
       	var newStr = str.replace(reg,function($,$1){
       		return $1.toUpperCase();
       	});
       	console.log(newStr);
```
2. 对数组去重？
```javascript
		var str = "aaaaaaaaaaabbbbbbbbbcccccccc";
        var reg = /(\w)\1*/g;
        console.log(str.replace(reg,"$1"));
```
3. 请将aaaaaabbbbbb的字符串调换成bbbbbbaaaaaa的形式？
```javascript
        var reg = /(\w{6})(\w{6})/g;
        var str = "aaaaaabbbbbb";
        console.log(str.replace(reg,"$2$1"));
```
4. 用**.**将str字符串从后向前3位3位截断？

```javascript
var reg = /(?=(\B)(\d{3})+$)/g;
var str = "1000000000";
console.log(str.replace(reg,"."));
```
5. 如何获取一个字符串中的数字字符，并以数组形式输出，如dgfhfgh234bhku259fakhdy678fh输出的是[234,259,678];

```javascript
var str = "dgfhfgh234bhku259fakhdy678fh";
var newArr = str.match(/\d+/g).map(function(x){
		return +x;
	})
console.log(newArr);
//ES6做法

```




><span style="font-size:12px">
>文章标题: <a href="{{permalink}}">{{ title }}</a>
>文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
>许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
>		  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
></span>