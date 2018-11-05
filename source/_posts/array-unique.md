---
title: 数组去重
date: 2015-05-27 05:05:04
tags: 代码片段
---

基本类型数组去重

* 方法一：

```javascript
function unique(array) {
  return Array.from(new Set(array))
}
```

* 方法二：

```javascript
function unique(array) {
  let res = [];
  array.forEach((item) => {
    if (res.indexOf(item) < 0) {
      res.push(item);
    }
  })
  return res;
}

```

