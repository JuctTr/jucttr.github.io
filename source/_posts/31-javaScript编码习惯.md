---
'title: 31.日常编码习惯
categories: 前端
date: 2019-11-30 16:40:09
tags: [javascript]
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# 文件名

1. 文件名的命名规范统一用`小写的字母且具有实际含义的单词`来命名。
2. 假如有两个单词，我们以`-`来分隔，如：`group-manage`。
3. 

# JavaScript

1. JavaScript 中 应当尽量少用全局变量，代码质量可以用全局变量和函数的数量来考量（数量越多越糟）。因此，尽可能避免使用全局变量。
2. 一些被拿过来渲染在页面中的数据，比如：Vue.js组件的data对象中的数据，小程序组件中的`properties和data对象`中，我们使用`驼峰式命名`的方式，`groupManage、periodTitle`。
3. 

# css

1. 选择器的命名规范，统一用中横线连接`-`，比如`class="group-manage"`，`class="activity-box"`
2. 在组件的最外层的容器，统一用`当前页面的名称-container`来命名，比如有一个页面的名称叫`group`，那么我们就把它的类名命名为`class="group-container"`。
3. 



# 组件的高复用

小程序中的组件命名方式，统一采用`前缀-group`，如：`<w-group></w-group>`

## 特性：

### 拿来即用

- 子组件可以根据父组件传入的properties来判断，该用什么样是形式呈现页面。







><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>

