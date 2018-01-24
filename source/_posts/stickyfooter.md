---
title: CSS Sticky Footer 方法一
date: 2018-01-20 11:34:26
tags: [前端, CSS]
---

------

**把content和footer包在wrapper里面**

> 1. html、body设置height为100%
> 2. footer绝对定位于wrapper底部
> 3. 上面设置完成后，footer就可以一直保持在页面底部

问题：当窗口缩放时，会出现footer将内容遮住

解决：给wrapper一个padding-bottom，高度与footer的高度一致（适用于footer高度固定）

以下是源码，直接把内容拷贝到html文件中，在浏览器中查看效果

```html
<html>

<head>
  <meta charset='UTF-8' />
  <style type="text/css">
    html,
    body {
      height: 100%; /* firefox需要设置宽度 */
      min-height: 100%;
      padding: 0;
      margin: 0;
    }
    .wrapper {
      position: relative;
      min-height: 100%;
      padding-bottom: 64px;
      box-sizing: border-box;
    }
    .footer {
      width: 100%;
      background-color: wheat;
      text-align: center;
      padding: 20px 0;
      position: absolute;
      bottom: 0;
    }
    p {
      margin: 0;
      padding: 0;
    }
  </style>
</head>

<body>
  <div class='wrapper'>
    <div class='content'>
      <p>这是内容这是内容这是内容这是内容这是内容这是内容</p>
    </div>
    <div class='footer'>
      这是底部
    </div>
  </div>
</body>

</html>
```