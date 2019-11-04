---
layout:     post
title:      "Http相关技术"
subtitle:   " \"小计\""
date:       2019-01-12 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - csrf
    - http
---

# Http相关技术
## CSRF 
用户登录A，浏览器保存A的登录状况。
被不法网站B盯上，用户访问B。
B发送向A的请求，比如
```html
<img src="a.com">
```

预防：
1.请求中加referer，判断referer.
2.增加token,服务器端验证。

禁用掉cookie后，session是否可用。


## 修改cookie办法
在手机端vconsole调试时，清除cookie:
```javascript
// document.cookie = newCookie
document.cookie = 'isUpdate=1'
```
注意有的时候，控制不能生效，可能是path,可能是domain，使用的时候在*newCookie*中增加";path=/"或者";domain=*.com"
```javascript
// document.cookie = newCookie
document.cookie = 'isUpdate=1;path=/g'
```
## QPS
QPS:(Querys Per Second),表示每秒查询数，一般是信息检索系统中的统计术语(比如database和搜索引擎)。但是这个术语，经常被用于请求-响应系统中，正确的叫法为每秒请求数(requests per seconds:RPS)。

峰值QPS和机器计算公式:
原理：每天80%的访问集中在20%的时间里，这20%时间叫做峰值时间。
```
( 总PV数 * 80% ) / ( 每天秒数 * 20% ) = 峰值时间每秒请求数(QPS)
```

