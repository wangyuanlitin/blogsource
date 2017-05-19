---
title: javascript检测是否是移动设备
date: 2014-09-11 19:56:12
tags: [javascript, mobile]
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