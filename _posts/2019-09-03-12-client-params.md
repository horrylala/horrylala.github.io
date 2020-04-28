---
layout:     post
title:      "浏览器相关技术"
subtitle:   " \"浏览器\""
date:       2019-03-12 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - 滚动
    - 视口
---

# 浏览器相关技术

## 文档坐标和视口坐标
文档坐标，相对于在显示文档的左上角。
视口坐标，相对于可视区域文档的左上角。

当文档发生滚动时候，文档坐标保持不变，但是视口坐标发生改变。

## 滚动位置
在IE8以前，可以使用scrollLeft和scrollTop来获取滚动位置。
在新版浏览器，pageXOffset和pageYOffset可以获取滚动位置。

查询滚动条的位置：
```javascript
function getScrollOffsets (w) {
  w = w || window
  
  // 除ie8之前浏览器都支持此方法
  if (w.pageXOffset !== null){
    return {
      x: w.pageXOffset,
      y: w.pageYOffset
    }
  }

  // ie8以前标准模式下，使用document.documentElement
  var d = w.document
  if (document.compatMode === 'CSS1Compat') {
    return {
      x: d.documentElement.scrollLeft,
      y: d.documentElement.scrollTop
    }
  }

  // 怪异模式使用document.body
  return {
    x: d.body.scrollLeft,
    y: d.body.scrollTop
  }
}
```

查询视口的尺寸：
```javascript
/** 获取视口的尺寸 */
function getViewportSize (w) {
  w = w || window

  // ie8以前的除外
  if (w.innerWidth !== null) {
    return {
      width: w.innerWidth,
      height: w.innerHeight
    }
  }

  // 标准模式下
  var d = w.document
  if (document.compatMode === 'CSS1Compat') {
    return {
      width: d.documentElement.clientWidth,
      height: d.documentElement.clientHeight
    }
  }

  // 怪异模式
  return {
    width: d.body.clientWidth,
    height: d.body.clientHeight
  }
}
```

总结：
使用对象，
>* IE8之前，标准模式，使用*document.documentElement*
>* IE8之前，诡异模式，使用*document.body*
>* IE8之后，使用*window*

使用属性，
>* IE8之前，标准模式，使用*scrollLeft*和*clientWidth*
>* IE8之前，诡异模式，使用*scrollLeft*和*clientWidth*
>* IE8之后，使用*innerWidth*

## 查询元素尺寸
使用*getBoundingClientRect()*方法，获取当前元素的尺寸，可以获取当前元素在视口区的位置。

```javascript

```

## 判断元素是否在视口区域
```javascript
// 判断元素是否在视口区域
function isAtViewport (e) {
  // 元素的文档位置 > 滚动位置 + viewport
  var box = e.getBoundingClientRect()
  var scrollOffset = getScrollOffsets()
  var viewport = getViewportSize()
  if (box.y < scrollOffset.y + viewport.height) {
    console.log('at viewport')
    return true
  }
}
```

不考虑IE8，代码是：
```javascript
function isAtViewportSpecial (e) {
  // 元素的文档位置 > 滚动位置 + viewport
  var box = e.getBoundingClientRect()
  var scrollOffsetY = window.pageYOffset
  var viewportHeight = window.innerHeight
  if (box.y < scrollOffsetY + viewportHeight) {
    console.log('at viewport')
    return true
  }
}
```