---
layout: post
title:  "debounce throttle"
description: 函数节流防抖.
date:   2020-02-18 11:03:36 
categories: sumrise
---

# debounce && throttle
## 函数防抖--在一定时间内只触发一次
```js
const debounce = function (fn, delay) {
  let time
  return function () {
    let args = arguments //箭头函数没有arguments和this
    if (time) {
      clearTimeout(time)
    }
    time = setTimeout(() => {
      fn.apply(this, args)
    }, delay)
  }
}
```
## 函数节流--间隔一段时间执行一次
```js
const throttle = function (fn, delay) {
  let time
  return function () {
    let args = arguments //箭头函数没有arguments和this
    if (time) {
      return
    }
    time = setTimeout(() => {
      fn.apply(this, args)
      time = null
    }, delay)
  }
}

const throttletime = function (fn, delay) {
  let time = 0
  return function () {
    let args = arguments
    let now = Date.now()
    if (now - time > delay) {
      fn.apply(this, args)
      time = now
    }
  }
}

function foo(e){
	console.log(e)
}
element.addEventListener('input',debounce(foo,1200))
element.addEventListener('input',throttle(foo,1200))

```
1. 函数防抖应用场景
    1. 输入框输入搜索，用户一段时间内停止输入才开始输入
    2. 手机号邮箱验证同上
    3. 窗口大小调整，重新渲染
2. 函数节流应用场景
    1. 滚动加载
    2. 高频点击提交