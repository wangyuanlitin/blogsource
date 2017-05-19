---
title: 数组去重
date: 2015-05-27 05:05:04
tags: 代码片段
---

```javascript

// 去掉一组整型数组重复的值
function unique(array) {
  let res = [];
  array.map((item) => {
    if (res.indexOf(item) < 0) {
      res.push(item);
    }
  })
  return res;
}

```
