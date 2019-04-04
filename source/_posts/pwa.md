---
title: PWA学习
date: 2019-01-14 13:56:11
tags: 优化
---

------

### 1. 什么是PWA？
PWA不是指某一项技术，包含Service Worker（离线缓存）、App Manifest（桌面）、Push API（推送）、Notifcations API（通知）、Background Sync（弱网）等技术

在网页上，应用一些技术，可以实现离线、消息推送、桌面入口等功能，使WebApp更接近NativeApp

### 2. 使用 ?
Service Worker
App Manifest
Push API

注册脚本

```javascript
if ('serviceWorker' in navigator) {

}
```
为什么在load时候注册
scope
生命周期：
installing
activating
全局变量
self caches clients
3. PWA 的进阶
4. PWA 与 Web 性能优化的结合