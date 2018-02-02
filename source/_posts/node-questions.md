---
title: Node.js 开发问题，不断更新
date: 2017-04-20 14:19:28
tags: [Node.js, Promise]
---

最近在重构一些之前的功能，项目用的是Node.js + express，发现很多问题

## 问题 List

### 1. promise timeout

```javascript
  function doWhatEver(){
    doSomeThing().then((res) => {
      let result = doOtherSomeThing();
      resolve(result);
    }, (error) => {
      reject(error);
    })
  }

```
<!--more-->
这个方法很简单，doSomeThing操作完后，doOtherSomeThing对结果进行操作，结果以promise返回；
没有考虑的问题，如果doSomeThing 没有返回，一直处在pending状态，doOtherSomeThing执行不到，也不会执行到resolve和reject状态，就会影响到其他的操作

### 解决办法1: promise设置一个timeout

```javascript
function timeout(ms, promise) {
  return new Promise((resolve, reject) => {
    promise.then(resolve);
    setTimeout(() => {
      reject(`${ms} timeout`)
    }, ms)
  })
}

```

那么上面这种情况就很简单，

```javascript

<!-- 用timeout方法包一下 -->

timeout(10 * 1000, doWhatEver)
  .then((res) => {
    resolve(res)
  })
  .catch((error) => {
    reject(error)
  })

```
