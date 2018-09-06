---
title: 持续动画效果的实现
date: 2018-05-07 15:56:50
tags: CSS
---

------

### 1. CSS实现

animate所包含的６个属性值

|      值       |    描述      |　值/例子 |
|-------------| -------------   |
| animation-name   　　　　　　　| 绑定到选择器的keyframe 名称   | animate-name: move; <br/> @keyframes move { <br/>  from { left: 0px} <br/>to {left: 200px}<br/>}<br/> from to 默认是从0%到100% , 也可以指定具体进度的动画效果　@keyframes move { <br/> 0% { left: 0px} <br/>50% {left: 100px} <br/>100% {left: 200px}<br/>}<br/>|
| animation-duration    　　　　| 动画完成要花费的时间          | 默认是0，没有动画，可以定义秒或者是毫秒，m或者是ms|
| animation-timing-function    | 速度曲线                    | linear	动画从头到尾的速度是相同的<br/>ease	默认。动画以低速开始，然后加快，在结束前变慢<br/>ease-in	动画以低速开始<br/>ease-out	动画以低速结束<br/>ease-in-out	动画以低速开始和结束<br/>cubic-bezier 我理解是自定义动画速度曲线 [例子](http://yisibl.github.io/cubic-bezier/#.17,.67,.83,.67)　|
| animation-delay  　　　　　　　|动画开始之前的延迟时间          | 默认是0，可以为负值 |
| animation-iteration-count 　　| 动画播放次数                 | 数值，或者是infinite(无限次播放)|
| animation-direction 　　　　　　| 是否要反向播放               | normal：正常播放（默认）；　alternate: 轮流反向播放|

<!--more-->

#### 例子

<iframe height='400' scrolling='no' title='css-animate' src='//codepen.io/wangyuanlitin/embed/aGVZON/?height=300&theme-id=32936&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/wangyuanlitin/pen/aGVZON/'>css-animate</a> by wangyuanli (<a href='https://codepen.io/wangyuanlitin'>@wangyuanlitin</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 2. setInterval实现

<iframe height='300' scrolling='no' title='js-animate' src='//codepen.io/wangyuanlitin/embed/ELbgoR/?height=300&theme-id=32936&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/wangyuanlitin/pen/ELbgoR/'>js-animate</a> by wangyuanli (<a href='https://codepen.io/wangyuanlitin'>@wangyuanlitin</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 3. requestAnimationFrame 实现
<iframe height='300' scrolling='no' title='MGOjXO' src='//codepen.io/wangyuanlitin/embed/MGOjXO/?height=300&theme-id=32936&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/wangyuanlitin/pen/MGOjXO/'>MGOjXO</a> by wangyuanli (<a href='https://codepen.io/wangyuanlitin'>@wangyuanlitin</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

### 总结

CSS animate：　CSS3属性，支持CSS3的浏览器都支持，提供丰富的属性可供选择，写法简单，可以处理一些简单的动画效果
setInterval：　JavaScript基本方法，支持性好，但是各个浏览器处理定时器时延时不一致，需要计算最优间隔时间，可能会造成卡顿现象，影响用户体验
requestAnimationFrame：浏览器专门为动画提供的API，重绘或回流的时间间隔紧紧跟随浏览器的刷新频率