---
title: CSS Sticky Footer 方法一
date: 2018-01-20 11:34:26
tags: [前端, CSS]
---

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