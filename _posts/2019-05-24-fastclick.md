---
layout:     post
title:      "一个由Fastclick产生的Bug"
subtitle:   " \"看似简单的问题，其实不简单\""
date:       2019-05-24 22:14:00
author:     "Horrylala"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - fastclick
    - bug
    - a
---

# FastClick遇到的问题

## 问题描述
>有这样一个场景：在前端页面中，有一个打电话的功能.

最简单的实现方法是：
```html
<a href="tel:12345678">呼叫小哥哥</a>
```

如果电话号码是通过后台接口返回的怎么处理呢？
```javascript
const ele = document.createElement('a')
ele.href = `tel:18238816509`
ele.innerText='打电话'
document.body.appendChild(ele)
ele.click()
document.body.removeChild(ele)
```
看起来简单，对吧？

但是，如果引入了FastCkick之后，上面的代码会执行吗，会调起电话吗？

## 问题定位
查看FastClick源码之后，
```javascript
  // touchend 时候，会执行sendClick
	FastClick.prototype.onTouchEnd = function(event) {
    // ...
    if (!this.needsClick(targetElement)) {
			event.preventDefault();
			this.sendClick(targetElement, event);
		}
    // ...
  }

  // sendClick会创建event事件进行执行
  FastClick.prototype.sendClick = function(targetElement, event) {
		var clickEvent, touch;

		// On some Android devices activeElement needs to be blurred otherwise the synthetic click will have no effect (#24)
		if (document.activeElement && document.activeElement !== targetElement) {
			document.activeElement.blur();
		}

		touch = event.changedTouches[0];

		// Synthesise a click event, with an extra attribute so it can be tracked
		clickEvent = document.createEvent('MouseEvents');
		clickEvent.initMouseEvent(this.determineEventType(targetElement), true, true, window, 1, touch.screenX, touch.screenY, touch.clientX, touch.clientY, false, false, false, false, 0, null);
		clickEvent.forwardedTouchEvent = true;
		targetElement.dispatchEvent(clickEvent);
  };
  
  // 然后执行onclick事件
  	FastClick.prototype.onClick = function(event) {
      // ...
    }
```

对于一个正常的页面标签，click事件会出发onTouchEnd(),sendClick()和onclick()。但是在代码中直接onclick无法触发sendClick事件中的dispatchEvent事件。

所以点击一次是无法调出打电话页面，是因为没有dispatchEvent。

有的同学会发现，双击两次是可以的。
是因为进入了
```javascript
	FastClick.prototype.onMouse = function(event) {
    // ...
    	if (!this.needsClick(this.targetElement) || this.cancelNextClick) {

			// Prevent any user-added listeners declared on FastClick element from being fired.
			if (event.stopImmediatePropagation) {
        // 进入了这里
				event.stopImmediatePropagation();
			} else {

				// Part of the hack for browsers that don't support Event#stopImmediatePropagation (e.g. Android 2)
				event.propagationStopped = true;
			}

			// Cancel the event
			event.stopPropagation();
			event.preventDefault();

			return false;
		}
    // ...
  }
```

## 解决办法
> 方法一：
```html
<a id="myId"></a>
```
```javascript
let idEl = document.getElementById('myId')
idEl.href = 'tel:12345678'
idEl.click()
```

> 方法二：
```javascript
const ele = document.createElement('a')
ele.href = `tel:18238816509`
ele.innerText='打电话'
document.body.appendChild(ele)
let evt = document.createEvent('MouseEvent')
evt.initMouseEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null)
evt.forwardedTouchEvent = true
ele.dispatchEvent(evt)
document.body.removeChild(ele)
```

## 总结
有些看似很简单的问题，其实并不简单。
对有疑问的地方，保持疑问。
> 问题：为什么两次点击是可以成功调起呼叫电话功能呢？

