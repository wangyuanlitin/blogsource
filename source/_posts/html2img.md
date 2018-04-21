---
title: DOM 转 图片
date: 2018-04-21 18:57:49
tags: JavaScript
---

------

因业务需要-每个用户都可以生成自己专属的图片信息， 实现方案-将用户信息转成图片，
对比了两个库， dom-to-image和html2canvas，基本都可以实现功能，但是还有一些差别

### 1. dom-to-image

```javascript
// 这是domtoimage的Demo
let dom = document.getElementById('my-node')

domtoimage.toPng(dom).then((dataurl) => { })
domtoimage.toJpeg(dom).then((dataurl) => { })
domtoimage.toBlob(dom).then((dataurl) => { })
domtoimage.toSvg(dom).then((dataurl) => { })
domtoimage.toPixelData(dom).then((dataurl) => { })
// 这么多API，但是不支持IOS，就会变的毫无意义

```

相比dom-to-image，html2canvas兼容性就稍微好点
<!--more-->
### 2. html2canvas
```javascript
// 这是html2canvas的Demo
let dom = document.getElementById('my-node')
html2canvas(dom).then((canvas) => {
    // 这里可以做一些操作
})

```
一些很有用的参数
allowTaint 是否允许加载其他域的图片生成canvas，如果允许的话，在canvas.toDataURL()的时候会提示跨域
logging    是否打印日志
useCORS    是否允许从服务端加载图片
width      生成canvas的宽度
height     生成canvas的高度
scale      生成图片的比例，默认按照设备显示


### 3. canvas使用toDataURL()的时候，提示跨域

为什么会跨域：
因为在dom中使用了别的域名的图片资源，虽然可以绘制canvas，但是这个时候canvas已经被污染，出于安全因素的考虑，在转图片的过程中会报错

解决办法：
1. 图片服务器设置Access-Control-Allow-Origin响应头
这个方法，不可能实现，因为图片来自微信头像
2. 将图片资源保存到本地服务器
和上面一个解决办法一样，不太可能
3. 在不让后端干涉的情况下，前端自己将图片转成base64或者是二进制流
base64有两种转换方式，通过blob转，或者是canvas
base64仍然有跨域的问题，远程图片转canvas又会涉及到画布被污染的问题，还是不可以使用toDataURL()方法
4. 后端转（最后解决方案）
后端直接提供接口，将图片转成二进制流
