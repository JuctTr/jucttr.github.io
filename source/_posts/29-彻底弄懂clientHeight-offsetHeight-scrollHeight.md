---
title: '29.彻底弄懂clientHeight,offsetHeight,scrollHeight'
categories: 前端
date: 2019-09-07 09:35:29
tags: [JavaScript,DOM]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# clientHeight

**特点：**只读属性

**概念：**元素内部的高度(单位像素)，包含内边距，但不包括水平滚动条、边框和外边距。

即是：clientHeight = height + padding-top + padding-bottom  

![clientHeight](https://o0zqrw.bn.files.1drv.com/y4mGLFYhbajPOYQwV2kvQ2GsWArqBrufUarAkKec4T_rGHuW4jiowVuDfwmTJJAavASjuV-Jp0YdHc2R0CYvV7pASTxxNdgiEdXGEr9JGVBCETH8KE-sa0blLHNwne5JBR1_rpsY1bfRVB1ORnnLGUmxYq7KRSTSngBPHafWz0ClQjs5S8DaTGUH6kDyWFreMVdXNQqVsQG9qttMKJJiFinpg?width=411&height=247&cropmode=none)

**拓展：**

1. clientWidth = width + padding-left + padding-right  ； `注意：clientWidth 不包括滚动条的宽度`
2. clientTop 等于 border-top
3. clientLeft 等于 border-left



# offsetHeight

**特点：**只读属性

**概念：**该元素的像素高度，高度包含该元素的垂直内边距和边框，且是一个整数。

即是：offsetHeight= height + padding + border



![offsetHeight](https://o0zquq.bn.files.1drv.com/y4mszPDssRAc5om9JCJplMIR2F3rkK34GsqLzqD9TxUUCgXochGzAubyM2Mvk-AdpvjsoIgFzV21LREsKVqsSxnpgvwpMQXfegdg7J6w_WUZYNWUDsN0hmMbhtvk_y_ZeVda-ZZD5wjPj07WWXVzlYk3luwpOxVyE1GxK-c07dvHpFfMxBrSGjk5EwGzYTU0E_Ob2GhAGl9FUGx1fr1inYKYA?width=411&height=247&cropmode=none)



**拓展：**

1. offsetWidth = width + padding + 竖直方向滚动条(scrollbar)宽度 + border 



# scrollHeight

**概念：**一个元素内容高度的度量，包括由于溢出导致的视图中不可见内容。也就是内容太多，导致出现滚动条，那些不可见的内容都会算进`scrollHeight`里面（包含滚动区域）



> **参考：**https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollHeight



# offsetLeft和offsetTop

**特点：**只读属性

**概念：**偏移量，offsetLeft 返回当前元素的上一级定位元素的左边缘，offsetTop 返回当前元素的上一级定位元素的上边缘，offsetLeft值跟offsetTop值的获取跟父级元素没关系，而是跟其上一级的**定位元素**(除position:static;外的所有定位如fixed,relative,absolute)有关系。



>**参考：**https://blog.csdn.net/w390058785/article/details/80461845






><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>