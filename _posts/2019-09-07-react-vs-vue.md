---
layout:     post
title:      "React和Vue的相同点和不同点"
subtitle:   " \"一直打算找个时间，梳理下react和vue的异同，今天终于有时间了\""
date:       2019-09-07 16:14:00
author:     "Horrylala"
header-img: "img/post-bg-os-metro.jpg"
catalog: true
tags:
    - Frameworks
    - React
    - Vue
    - JavaScript
---

## 相同点

### Virtual Dom的概念
### 组件化
### Cli
React使用create-react-app(CRA)快速构建。
Vue使用vue-cli快速构建。

### 调试工具
React和Vue都有Chrome扩展工具，以方便调试。
具体使用方法，可在Chrome Extension中找到对应的调试工具。
Vue调试工具[Vue.js devtools](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en-US)
React调试工具[React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en-US)

### 相关联的开发库
React和Vue都有相关联的库，比如状态管理和router等。

### 原生友好
React有React-native，Vue有Weex。

## 不同点

### JSX vs 模板
React采用JSX语法，使用的是all-in-js的思想。
Vue采用模板语法，侧重在关注点分离，视图层解决视图的问题，逻辑层解决逻辑问题，当然，Vue也提供JSX语法。

### 单向数据流和双向绑定
React采用单向数据流，在setState之后，会重新render更新视图，如果shouldComponentUpdate是false就不会重新渲染。
Vue使用Object.defineProperty对props和data中的数据进行监听绑定，当逻辑层的数据发生改变，那么就会重新出发页面的render。
所以，React中，数据改变是view = f(state)，调用函数。
Vue中，数据改变是Object.definProperty进行处理。

### 社区贡献
React负责核心功能，其他边缘库交给社区做。
Vue继承了大部分功能，官方库。
