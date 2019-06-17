---
layout:     post
title:      "微信7.0软键盘弹起不自动弹回"
subtitle:   " \"Hello World, 第一篇博客\""
date:       2019-01-05 16:51:00
author:     "Horrylala"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Wechat
    - Keybord
---

## 问题描述
---
```
微信公众号页面，input输入弹起软键盘，完成输入后，页面没有还原。
微信版本： 6.7.4, 7.0.0
系统类型：IOS(安卓正常)
```

问题分析：
1. 1.弹起软键盘之后，页面没有执行resize操作

官方资料：
1. 1.IOS升级到12.0+时候，xcode打包产生的webview bug
2. 2.6.7.3出现的问题，在7.0.0仍然没有解决

## 解决方案
input失焦时，重新出发页面的resize，比如scrollTop
```javascript
onBlur () {
  // add personal handle
  document.body && (document.body.scrollTop = document.body.scrollTop)
}
```

## document.body.scrollTop 和 document.documentElement.scrollTop
在谷歌上，*document.body.scrollTop*一直返回的是0，但是*document.documentElement.scrollTop*能获取到真实的数据。

[网上](https://blog.csdn.net/tfgdd/article/details/5182033)的(未找到官方说明)解释是：
```
documentElement 对应的是 html 标签，而 body 对应的是 body 标签。
在标准w3c下，document.body.scrollTop恒为0，需要用document.documentElement.scrollTop来代替。
```

但是在实际的公众号中，*document.documentElement.scrollTop*一直返回的是0，但是*document.body.scrollTop*能获取到真实的数据。





