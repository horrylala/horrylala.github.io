---
layout:     post
title:      "微前端"
subtitle:   " \"微前端，在路上\""
date:       2019-12-31 21:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - 微前端
    - Javascript
---

# 微前端
[微前端](https://www.thoughtworks.com/radar/techniques/micro-frontends)是由ThoughtWorks 在2016年提出的。
在2016年的[technolody-radar](https://assets.thoughtworks.com/assets/technology-radar-nov-2016-en.pdf)中，关于微前端，描述为：
> In this approach, a web application is broken up by its pages and features, with each feature being owned end-to-end by a single team. 

![img](/img/radar.png)
翻译为中文为：
> 单一的Web应用转换为多个小型前端应用聚合一体，每个小型应用由单独的团队运作。

## 优势

## 微前端设计方法
单一的web前端应用如何拆解为多个应用呢？

如果需要将一个大型应用拆分成多个小型应用，那么就需要组织多个应用之间的交互。


## 微前端有哪些实现方式
其中主要的方案：
1.iframe
2.JavaScript
3.Web Component

### 通过iframes
如下是一个简单的实现方案:
```html
<html>
  <head>
    <title>Micro Front</title>
  </head>
  <body>
    <h1>Micro Front Demo using iframe</h1>
    <iframe id="micro-front-container"></iframe>
    <script>
      const microFrontByRoutes = {
        '/': 'https://browse.example.com/index.html',
        '/order-food': 'https://order.example.com/index.html',
        '/user-profile': 'https://profile.example.com/index.html',
      }
      const iframe = document.getElementById('micro-front-container')
      iframe.src = microFrontByRoutes[window.location.pathname]
    </script>
  </body>
</html>
```
定义好每个路由的请求链接，根据路由返回不同的页面。

这种方式比较容易实现，但是问题是：
* 这种子项目不能带导航
* iframe嵌入的显示区域不受控制，页面刷新不存储状态
* 样式兼容
* 页面返回前进后退不易于控制

### 通过JavaScript
通过不同路由，执行不同的js显示不同的页面控制。
```html
<html>
  <head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <!-- These scripts don't render anything immediately -->
    <!-- Instead they attach entry-point functions to `window` -->
    <script src="https://browse.example.com/bundle.js"></script>
    <script src="https://order.example.com/bundle.js"></script>
    <script src="https://profile.example.com/bundle.js"></script>

    <div id="micro-frontend-root"></div>

    <script type="text/javascript">
      // These global functions are attached to window by the above scripts
      const microFrontendsByRoute = {
        '/': window.renderBrowseRestaurants,
        '/order-food': window.renderOrderFood,
        '/user-profile': window.renderUserProfile,
      };
      const renderFunction = microFrontendsByRoute[window.location.pathname];

      // Having determined the entry-point function, we now call it,
      // giving it the ID of the element where it should render itself
      renderFunction('micro-frontend-root');
    </script>
  </body>
</html>
```
这种是最具有灵活性，易于控制。

### 基于Web Component
这个是定一个Web组件，通过路由不同，显示不同的组件。
```html
<html>
  <head>
    <title>Feed me!</title>
  </head>
  <body>
    <h1>Welcome to Feed me!</h1>

    <!-- These scripts don't render anything immediately -->
    <!-- Instead they each define a custom element type -->
    <script src="https://browse.example.com/bundle.js"></script>
    <script src="https://order.example.com/bundle.js"></script>
    <script src="https://profile.example.com/bundle.js"></script>

    <div id="micro-frontend-root"></div>

    <script type="text/javascript">
      // These element types are defined by the above scripts
      const webComponentsByRoute = {
        '/': 'micro-frontend-browse-restaurants',
        '/order-food': 'micro-frontend-order-food',
        '/user-profile': 'micro-frontend-user-profile',
      };
      const webComponentType = webComponentsByRoute[window.location.pathname];

      // Having determined the right web component custom element type,
      // we now create an instance of it and attach it to the document
      const root = document.getElementById('micro-frontend-root');
      const webComponent = document.createElement(webComponentType);
      root.appendChild(webComponent);
    </script>
  </body>
</html>
```
这种方式也是可行的，主要基于Web component，如果是浏览器支持，也是一种很不错的方案。

## 微前端的挑战
微服务也有很多问题,比如重复的包引入、不同环境的影响、CI复杂度等问题。


## 总结
微前端是对单页面应用优化的一个很好的实践，有机会也有挑战。如果可以区分好边界，哪些适合做微前端，哪些不需要，那么微前端将是一个非常好的解决方案。

详细的案例可以参考[micro front](https://github.com/micro-frontends-demo).

参考链接：
* [实现微前端的六种方式](https://segmentfault.com/a/1190000015566927?utm_source=tag-newest)
* [Micro Frontends](https://martinfowler.com/articles/micro-frontends.html)
* [用微前端的方式搭建类单页应用](https://tech.meituan.com/2018/09/06/fe-tiny-spa.html)