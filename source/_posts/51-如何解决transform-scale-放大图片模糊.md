---
title: '51.如何解决transform: scale()放大图片模糊?'
categories: 前端
date: 2019-12-20 11:51:19
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

最终效果图

![](C:\Users\wangyicong5\AppData\Roaming\Typora\typora-user-images\scale()放大图片模糊.gif)

在使用这个`transform: scale()`的时候，有一个问题，就是当他放大的时候图片会模糊，我们先来看一个小栗子：

![放大10倍](C:\Users\wangyicong5\AppData\Roaming\Typora\typora-user-images\放大10倍.gif)

这个是在原来的基础上放大10倍，代码如下：

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .container {
      border: 1px solid red;
      width: 100px;
      height: 100px;
      animation: zoom 1s ease-in-out forwards;
      transform-origin: 0 0;
    }
    .container img {
      width: 50%;
    }
    @keyframes zoom {
      from { transform: scale(0);}
      to { transform: scale(10); }
    }
  </style>
</head>
<body>
  <div class="container">
    <img src="./首次进入的红包进度条/images/loading-红包-1.png" alt="">
  </div>
</body>
</html>
```

我们可以看到，动画在执行完的时候，会从最模糊的那一刻，出现一次抖动，然后变清晰了一点，这个现象目前我还不知道是为什么？

然后我们看一个，先把原来的放大10倍，在利用`transform: scale()`先缩小10倍，后面再在动画执行的时候在去放大图片



![先缩小在放大](C:\Users\wangyicong5\AppData\Roaming\Typora\typora-user-images\先缩小在放大.gif)

这样的方法，在最后的时刻，就不像上面那样，没有了一次抖动，相对来说比较平滑一点，效果也符合用户体验

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .container {
      border: 1px solid red;
      width: 1000px;
      height: 1000px;
      transform: scale(0.1);
      animation: zoom 1s ease-in-out forwards;
      transform-origin: 0 0;
    }
    .container img {
      width: 50%;
    }
    @keyframes zoom {
      from { transform: scale(0);}
      to { transform: scale(1); }
    }
  </style>
</head>
<body>
  <div class="container">
    <img src="./首次进入的红包进度条/images/loading-红包-1.png" alt="">
  </div>
</body>
</html>
```




><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>