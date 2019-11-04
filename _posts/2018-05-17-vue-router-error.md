---
layout:     post
title:      "vue开发问题"
subtitle:   " \"记录路上的坑\""
date:       2018-05-17 21:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - vue
    - prxoy
---

# vue开发问题
---
记录vue开发过程的一些问题。

## Uncaught SyntaxError: Unexpectedd token <
[vue-router] Filed to resolve aysnc component default: error :loading chunck 34 failed

* 问题描述：
打开页面，点击某些路由跳转，返回时资源加载失败。

![资源加载是吧](./img/20190309170418.png)

一般出现在后退按钮上，当返回时Js加载报错。
刷新之后，问题解决。

* 问题定位：

手机浏览器还没有关闭，仍然访问上一个页面，但是如果发布了新包，这个时候返回的时候就提示找不到资源。报错。

* 问题解决：

如何在用户无感知的情况下更新页面？或者解决用户问题？

> 在版本发布时，记录当前版本号，可以在每次路由的时候，加载一个很小的资源，请求最新版本，如果版本不一致，那么就刷新页面，重新加载。

## 热更新不更新
是因为设置了proxy:
```js
{
  '/': {
    target: 'https://a.test.com', // 测试环境
    changeOrigin: true
  }
}
```