---
title: Web通信之长轮询、长连接
date: 2017-07-24 18:42:15
tags: [前端, 通信,笔记]
---

需求：　为了减少账号的共用，在执行某项操作之前需要微信扫码验证才能进入，二维码没隔3s更新一次
实现：　前端和后端保持一个长连接，后端会定时发送唯一地址到前端，前端将地址转成二维码显示出来


在这之前没有接触过WebSocket之类的东西，也不清楚长连接和长轮询之间有什么区别，下面记录一下一些学习笔记


### 轮询
在特定的时间间隔(setInterval),　浏览器向服务器发送HTTP请求，服务器返回结果
缺点：实现实时性不高，服务器压力大。
实现：

```javascript
setInterval(function(){
	ajax({
		type: 'get',
		url: url
	})
}, 5 * 1000)
```

### 长轮询
客户端向服务器发送Ajax请求，服务端返回结果，断开连接，直到客户端处理完后，才发送下次请求

优点：在无消息的情况下不会频繁的请求，耗费资源小，实时性比较高，延迟小。
缺点：服务器hold连接会消耗资源，返回数据顺序无保证，难于管理维护。 
请求：多次
实例：WebQQ、Hi网页版、Facebook IM
<!--more-->
实现：

```javascript
function get(){
	ajax({
		type: 'get',
		url: url,
		success: function(res) {
			get();//有结果返回时，开始下一次请求ｉ
		}
	})
}
```

### 短连接
普通的TCP连接

### 长连接
在页面里嵌入一个隐蔵iframe，将这个隐蔵iframe的src属性设为对一个长连接的请求，服务器端就能源源不断地往客户端输入数据。

优点：消息即时到达，不发无用请求；管理起来也相对方便。 
缺点：服务器维护一个长连接会增加开销。 
请求：长连接其实只有一次请求
实例：Gmail聊天
实现：javascript原生WebSocket
```javascript
var socket = new WebSocket('ws://localhost:8080'); 
socket.onopen = function(event) { 
  socket.send('I am the client and I\'m listening!'); 
  socket.onmessage = function(event) { 
    console.log('Client received a message',event); 
  }; 

  socket.onclose = function(event) { 
    console.log('Client notified socket has closed',event); 
  }; 

  socket.close() 
};
```
除了上述方法，还可以借助一些socket.io的库来实现，也可以使用iframe