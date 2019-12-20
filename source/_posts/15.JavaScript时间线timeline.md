---
title: JavaScript时间线timeline
categories: 前端
date: 2019-04-13 10:27:33
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

# TimeLine

## 什么是JavaScript时间线？

**时间线**也可以理解为记录浏览器加载页面一系列发生的过程。

## 时间线分为哪几个过程？

一般分为十个步骤：

1. 创建 Document 对象，开始解析 web 页面。解析 HTML 元素和他们的文本内容，后添加 Element 对象和 Text 节点到文档中。这个阶段 document.readyState ='loading'。
2. 遇到 link 外部 css，创建线程，进行异步加载，并继续解析文档。
3. 遇到 script 外部 js，并且没有设置 async、defer，浏览器同步加载，并阻塞，等待 js 加载完成并执行该脚本，然后继续解析文档。
4. 遇到 script 外部 js，如果是设置有 async、defer，浏览器创建线程异步加载，并继续解析文档。对于 async属性的脚本，脚本加载完成后立即执行。 （异步禁止使用document.write()，因为当你整个文档解析到差不多，再调用 document.write()，会把之前所有的文档流都清空，用它里面的文档代替）
5. 遇到 img 等（带有 src），先正常解析 dom 结构，然后浏览器异步加载 src，并继续解析文档。
6. 当文档解析完成（DomTree 建立完毕，不是加载完毕），此时document.readyState ='interactive'。
7. 文档解析完成后，所有设置有 defer 的脚本会按照顺序执行。（注意与 async 的不同,但同样禁止使用 document.write()）
8. document 对象触发 DOMContentLoaded 事件，这也标志着程序执行从同步脚本执行阶段，转化为事件驱动阶段。
9. 当所有 async 的脚本加载完成并执行后、img 等加载完成后（页面所有的都执行加载完之后），document.readyState = 'complete'，window 对象触发 load 事件。
10. 从此，以异步响应方式处理用户输入、网络事件等。

## 如何使用Chrome开发者工具中的timeline？

[timeline的使用](https://developers.google.com/web/tools/chrome-devtools/memory-problems/)






><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>