---
layout:     post
title:      "如何预防xss攻击"
subtitle:   " \"我又回来了\""
date:       2019-03-15 22:14:00
author:     "Horrylala"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - xss
    - 网络安全
    - http
---

# 什么是xss
XSS是跨站脚本攻击(Cross Site Scripting)简写，为了不和层叠样式表(CSS)混写，所以写为XSS。

最常见的xss攻击是在input输入框中，输入非法的代码，如果这段代码保存了，那么其他用户登录此网站，打开某个网页，就会弹出一些非法的代码。

# xss一些常见分类
## 存储型
注入的脚本存储在数据库中，用户访问攻击网站获取用户信息，比如发帖等

## 反射型
构造特殊url，用户打开url执行特殊操作，获取用户信息等，比如搜索，跳转

## DOM型
在前端执行，因此不要不可信的内容作为html插入到页面。，比如.innerHtml/.outerHtml/document.write或者VUE中的v-html

# 预防办法
1.对输入的内容进行转义：'<'、'>'、'&'、' '等，使用escapeHTML
```javascript
a.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&apos;")
```
2.长度校验
3.非法schema,禁止以javascript开头的
4.CSP
CSP(ontent Security Policy,内容安全策略)，是为了解决网络安全提出的内容策略。
可以设置：
禁止加载外域代码
合理上报问题的xss，及时修复
禁止内联脚本执行




