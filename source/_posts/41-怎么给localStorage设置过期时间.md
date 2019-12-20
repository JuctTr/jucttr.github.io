---
title: 41.怎么给localStorage设置过期时间?
categories: 前端
date: 2019-09-30 22:48:11
tags:
---
在学习JavaScript的一些总结和经验，供大家参考和学习，同时也欢迎大家参与讨论。

<!--more-->

设置一个时间戳，在取值的时候，判断当前时间（nowTime）和当时存入的数据的过期时间（expireTime）的大小；

下面这个还有待完善：

- 过期时间的输入是以天、小时、分钟、秒或者毫秒为单位？
- 又或者是存的是图片，需要把图片转为base64编码等等
- 

```javascript
var storageUtil = {
    setItem: function (key, value, expireTime) {
        try {
            if (typeof expireTime != 'number') {
                throw new Error('请检查格式是否输入正确，设置的日期格式必须是数字！');
            }
            var cacheExpireTime = new Date().getTime() + expireTime;

            var params = { data: value, expireTime: cacheExpireTime };
            localStorage.setItem(key, JSON.stringify(params)); 
            // 之所以用JSON.stringify()是因为传进来的value可能是对象类型
        } catch (error) {
            console.log(error);
        }
    },
    getItem: function(key) {
        try {
            var nowTime = new Date().getTime();
            var params = localStorage.getItem(key);
            var obj = JSON.parse(params);

            if (nowTime > obj.expireTime) {
                this.removeItem(key);
                return "";
            }
            return obj.data;
        } catch (error) {

        }
    },
    removeItem: function(key) {
        localStorage.removeItem(key);
    },
    clear: function() {
        localStorage.clear();
    }
}
```





> 参考：<https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/171>

-------------------------------------


><span style="font-size:12px">
	文章标题: <a href="{{permalink}}">{{ title }}</a>
	文章作者: <a href="https://github.com/WangYiCong">王奕聪，QQ:1301842163</a>  
	许可协议: <img src="https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png" style="display: inline !important;margin:0;padding:0;" alt="知识共享许可协议">
			  <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">©署名-非商用-相同方式共享 4.0</a>
</span>

