---
title: 47.常用的Sass语法
categories: 前端
date: 2019-12-06 17:53:13
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# 常用的Sass语法

## 一、最常用的嵌套规则

```scss
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
/* 相当于(编译后) */
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }

```



## 二、引用变量

变量以$开头，至于单词间以  ` - `  或者  ` _ `  间隔，取决于个人爱好，提倡以中横线  -  间隔

```scss

$nav-color: #F90;
nav {
  $width: 100px;
  width: $width;
  color: $nav-color;
}
//编译后
nav {
  width: 100px;
  color: #F90;
}

$highlight-color: #F90;
.selected {
  border: 1px solid $highlight-color;
}
//编译后
.selected {
  border: 1px solid #F90;
}

```



## 三、父选择器的标识符  &  

```html
<div class="nav">
   <div class="nav_item">
    	<a href="#"></a>
    </div>
   <div class="nav_item">
    	<a href="#"></a>
    </div>
   <div class="nav_item">
    	<a href="#"></a>
    </div>
</div>

<style>
    .nav {
        width: 100px;
        height: 100px;
        ....
        &_item {
           ...
        }
       / * 
        或者
        .nav_item {
            
        }
        * /
        .nav_item a {
            &:hover {
                
            }
        }
        &::before {
            ......
        }
    }
</style>
```

## 

## 四、导入SASS文件

```scss
@import '../common/styles/common'
// 或
@import '../common/styles/common.scss'
```



## 五、混合器

​	当你的项目越来越大，样式越来越复杂，像我们上面第二种`引用变量`这种独立的变量已经不能满足我们了，需要大段大段的重用（复用）样式的代码，我们可以通过`sass`的混合器实现大段样式的重用。

### 定义一个混合器

比如我们在一个common.scss文件定义一个混合器叫 `Mixin-Name`

```scss
@mixin Mixin-Name {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```

### 引用混合器

那么我们在index文件中就可以这样子使用`@include`引用

```scss
@import 'common.scss';
.className {
  background-color: green;
  border: 2px solid #00aa00;
  @include Mixin-Name; /* 引用 */
}
```

### 给混合器传参

```scss
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
// 应用场景：复用样式代码率高，定制化强！！！！！！！！！！
a {
  @include link-colors(blue, red, green);
}
//Sass最终编译后生成的是：
a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }
```



## 等等一些不常用的或者说用得少的

比如继承，控制指令、函数等






><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>