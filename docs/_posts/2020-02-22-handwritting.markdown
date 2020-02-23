---
layout: post
title:  "handwritting"
description: handwritting source code.
date:   2020-02-22 09:53:36 
categories: handwritting
---

# call,apply,bind

```js
//mycall
Function.prototype.mycall = function (ctx = window) {
  let args = [...arguments].slice(1)
  ctx.fn = this
  let resultFn = ctx.fn(...args)
  delete ctx.fn
  return resultFn
}
//myapply
Function.prototype.myapply = function (ctx = window) {
  ctx.fn = this
  let resultFn
  // 处理参数和 call 有区别 apply传入的是数组
  if (arguments[1]) {
    resultFn = ctx.fn(...arguments[1])
  } else {
    resultFn = ctx.fn()
  }
  delete ctx.fn
  return resultFn
}
//mybind
Function.prototype.mybind = function (ctx = window) {
  let arg = [...arguments].slice(1), _this = this
  return function () {
    //注意新函数传入的参数
    _this.apply(ctx, arg.concat(...arguments))
  }
}
```