---
title: javascript检测是否是移动设备
date: 2014-09-11 19:56:12
tags: javascript, mobile
---

### 1. https://web.wurfl.io/

```javascript

<script src="//wurfl.io/wurfl.js"></script>

```

WURFL.is_mobile                  判断是否是手机，返回true/false
WURFL.complete_device_name       获取手机具体型号


### 2. http://hgoebl.github.io/mobile-detect.js/

```javascript

<script src="mobile-detect.js"></script>

```

var info = new MobileDetect(window.navigator.userAgent);
info.os()                       获取手机操作系统
info.mobile()                   获取手机品牌（需要在js中写入判断）
info.phone()                    获取手机品牌（需要在js中写入判断）

info.is('iPhone')               判断是否是iphone设备






为简化原生app中的管理流程，专门开发的手机版系统，该系统使用到的技术栈react、redux、webpack、es6，scss等，前端页面使用material-ui，前端页面组件化提高重复利用和维护，redux合理管理状态，严格的代码检查，项目中熟悉了组件间通信和数据管理，了解redux原理