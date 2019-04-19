---
title: Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?
date: 2018-10-12 10:48:28
tags: [HTML5,编程,Web]
categories: 前端
---
在学习HTML和CSS的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# 一、Doctype作用是什么？

<!DOCTYPE>声明叫做文件类型定义（DTD），声明的作用为了告诉浏览器该文件的类型。让浏览器解析器知道应该用哪个规范来解析文档。<!DOCTYPE>声明必须在 HTML 文档的第一行，这并不是一个 HTML 标签。

# 二、严格模式与混杂模式如何区分？它们有何意义？

**严格模式：**又称标准模式，是指浏览器按照 W3C 标准解析代码。

**混杂模式：**又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。

**如何区分：**浏览器解析时到底使用严格模式还是混杂模式，与网页中的 DTD 直接相关。

1、如果文档包含严格的 DOCTYPE ，那么它一般以严格模式呈现。**（严格 DTD ——严格模式） **
2、包含过渡 DTD 和 URI 的 DOCTYPE ，也以严格模式呈现，但有过渡 DTD 而没有 URI **（统一资源标识符，就是声明最后的地址）** 会导致页面以混杂模式呈现。**（有 URI 的过渡 DTD ——严格模式；没有 URI 的过渡 DTD ——混杂模式） **
3、DOCTYPE 不存在或形式不正确会导致文档以混杂模式呈现。**（DTD不存在或者格式不正确——混杂模式）**
4、HTML5 没有 DTD ，因此也就没有严格模式与混杂模式的区别，HTML5 有相对宽松的语法，实现时，已经尽可能大的实现了向后兼容。**（ HTML5 没有严格和混杂之分）**

**意义：**严格模式与混杂模式存在的意义与其来源密切相关，如果说只存在严格模式，那么许多旧网站必然受到影响，如果只存在混杂模式，那么会回到当时浏览器大战时的混乱，每个浏览器都有自己的解析模式。

# 三、严格模式与混杂模式的语句解析不同点有哪些？

#### 1）盒模型的高宽包含内边距padding和边框border

![DOCTYPE作用](https://wx2.sinaimg.cn/mw690/006rmJyDgy1fw6eoiabaqj30i20bmdla.jpg)

>在W3C标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在IE5.5及以下的浏览器及其他版本的Quirks模式下，IE的宽度和高度还包含了padding和border。

#### 2）可以设置行内元素的高宽

    在Standards模式下，给span等行内元素设置wdith和height都不会生效，而在quirks模式下，则会生效。

#### 3）可设置百分比的高度

    在standards模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置高度，子元素设置一个百分比的高度是无效的。

#### 4）用margin:0 auto设置水平居中在IE下会失效

    使用margin:0 auto在standards模式下可以使元素水平居中，但在quirks模式下却会失效,quirk模式下的解决办法，用text-align属性:

	   body{text-align:center};#content{text-align:left}

#### 5）quirk模式下设置图片的padding会失效

#### 6）quirk模式下Table中的字体属性不能继承上层的设置

#### 7）quirk模式下white-space:pre会失效

># 补充内容：

# 一、常用的具体声明：

#### 1、HTML5（一种）：<!DOCTYPE html>

#### 2、HTML 4.01（三种）：严格模式包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font），不允许框架集（Framesets）；过渡模式包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font），不允许框架集（Framesets）；框架模式等同于过渡模式，但允许框架集内容。 

HTML 4.01 Strict ：<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

HTML 4.01 Transitional ：<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"  "http://www.w3.org/TR/html4/loose.dtd">

HTML 4.01 Frameset ：<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN"  "http://www.w3.org/TR/html4/frameset.dtd">

#### 3、XHTML 1.0（四种）：前三种模式同上，XHML 必须以格式正确的 XML 来编写标记。 

XHTML 1.0 Strict ：<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> 

XHTML 1.0 Transitional ：<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" " http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> 

XHTML 1.0 Frameset： <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd"> 

XHTML 1.1 该 DTD 等同于 XHTML 1.0 Strict，但允许添加模型。<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">

# 二、严格模式与混杂模式的来源

----
>当年Netscape4（网景公司早期的浏览器）和IE4（微软公司早期的浏览器）实现CSS机制时，并没有遵循W3C提出的标准。Netscape4 提供了糟糕的支持，而IE4 虽然接近标准，但依旧未能完全正确的支持标准。尽管IE 5 修复了IE4 许多的问题，但是依然延续CSS实现中的其它故障（主要是盒模型问题）。

----
>为了保障自己的网站在各个浏览器上显示正确，网页开发者们不得不依据各个浏览器自身的规范来使用css，因此大部分网站的css实现并不符合W3C规范的标准。

----
>然而随着标准一致性越来越重要，浏览器开发商不得不面临一个艰难的抉择：逐渐遵循W3C的标准是前进的方向。但是改变现有的 css，完全去遵循标准，会使许多旧网站或多或少受到破坏，如果浏览器突然以正确的方式解析现存的css，陈旧的网站的显示必然会受到影响。所以，所有的浏览器都需要提供两种模式：混杂模式服务于旧式规则，而严格模式服务于标准规则。

-----------

>**说明：**来自网络 https://www.cnblogs.com/wuqiutong/p/5986191.html

----------------

><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>