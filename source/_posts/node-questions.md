---
title: Node.js Promise 超时
date: 2017-04-20 14:19:28
tags:
---

------

最近在給之前做过的项目新增一些功能，是用Node.js + express构建的，发现很多问题都是自己埋的坑，额。。。。。感慨在一条错误的道路上走了这么久，也是挺不容易的。

## 最坑问题 List

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

这个方法很简单，doSomeThing操作完后，doOtherSomeThing对结果进行操作，结果以promise返回；重点问题来了，doSomeThing 没有返回，一直处在pending状态，doOtherSomeThing执行不到，也不会执行到resolve和reject状态，就会影响到其他的操作

### 解决办法1: promise设置一个timeout

```javascript

<!-- 这段代码是在别的地方看到的，但是忘记哪里了，如有冒犯，请联系删之 -->

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
