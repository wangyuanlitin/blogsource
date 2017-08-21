---
title: javascript "指南"
date: 2017-08-21 10:28:35
tags: [javascript]
---

[原文链接](https://github.com/jawil/blog/issues/24)

1、单行评级组件
```javascript
　"★★★★★☆☆☆☆☆".slice(5 - rate, 10 - rate);　rate是1到5的值
```
2、https://sdk.cn/news/3025

3、优雅的取随机字符串
```javascript
Math.random().toString(16).substring(2) // 13位
Math.random().toString(36).substring(2) // 11位
```