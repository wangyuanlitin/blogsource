---
title: Express V4.16.4
date: 2018-11-01 15:12:34
tags: JavaScript
---

------

最基本的express服务器搭建

```Javascript

const express = require('express')
const app = express() 

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```
<br/>
上面这段代码做了什么？
<br/>
2018.11.01 记录

---



1. 定义express对象
2. 定义路由
3. 启动服务
<!--more-->
##### 第一部分

const app = express()

```Javascript
// 入口方法
function createApplication() {
  // 没看明白这种写法
  // 定义app方法，调用app.handle
  var app = function (req, res, next) {
    app.handle(req, res, next);
  };

  /*
   * mixin 是一个库 merge-descriptors
   * 把第二个参数合并到第一个参数， false 如果第一个参数有相同key，那就跳过，不覆盖
   */
  mixin(app, EventEmitter.prototype, false); // node event 原生的参数

  mixin(app, proto, false); // proto 定义了公共的api，比如经常用到的app.use()、app.all()、app.handle()、app.listen() ...

  // app.request 是 req的值，同时又将app挂到req下
  // 但是好像没理解实质， --- 应该是app.request集成自req，基本写法var a = Object.create(b),
  app.request = Object.create(req, {
    app: { configurable: true, enumerable: true, writable: true, value: app }
  })
  

  /*
   * req定义的类似这么一窝东西，从哪里取的呢？应该是从http.IncomingMessage.prototype这个里面取的，这个值里面有什么，没看
   * console.log(req.protocol);
   * console.log(req.secure);
   * console.log(req.ip);
   * console.log(req.ips);
   * console.log(req.hostname);
   * console.log(req.fresh);
   * console.log(req.xhr);
   * console.log(req.header('Connection'));
   * console.log(req.accepts());
   */

  app.response = Object.create(res, {
    app: { configurable: true, enumerable: true, writable: true, value: app }
  })
  /*
   * res 同样设置了一堆返回的东西，应该是从http.ServerResponse.prototype这个里面取的，具体也没看
   * res.status(code) 设置statusCode
   * res.send(body) 设置返回的值，可以穿两个值，第一个是body， 第二个是statusCode; 也可以之间返回statusCode
   * res.json(obj) 最后还是调用res.send()， 区别应该是多了一堆setting，不想看了
   * res.jsonp(obj) 也是多了一堆设置，header设置，Content-Type 看一下
   * res.sendStatus(statusCode) 和 res.send(statusCode) 也没啥区别，比send更纯粹？？？？
   * res.sendFile res.download 一个是文件流，一个是直接下载？？？？？没多看，但是header 头不一样
   * res.cookie()
   * res.redirect()
   * res.render() // 按照那个模版渲染
   */ 

  app.init();
  /*  设置头response信息
   *  监听mount事件
   */

  return app;
}
// 定义路由，定义app[method] 调用route里面定义的
methods.forEach(function (method) {
  app[method] = function (path) {
    if (method === 'get' && arguments.length === 1) {
      // app.get(setting)
      return this.set(path);
    }

    this.lazyrouter(); // 创建this._router

    var route = this._router.route(path);
    route[method].apply(route, slice.call(arguments, 1));
    return this;
  };
});
// 定义this._router
app.lazyrouter = function lazyrouter() {
  if (!this._router) {
    this._router = new Router({
      caseSensitive: this.enabled('case sensitive routing'),
      strict: this.enabled('strict routing')
    });

    this._router.use(query(this.get('query parser fn')));
    this._router.use(middleware.init(this)); // middleware.init(this) 做了什么
  }
};
```

<br/>

2018.11.05 记录

---

##### 第二部分

app.get('/', (req, res) => res.send('Hello World!'))

```javascript
// 调用定义好的app.get方法，app.get调用route对应的方法
methods.forEach(function (method) {
  Route.prototype[method] = function () {
    var handles = flatten(slice.call(arguments));

    for (var i = 0; i < handles.length; i++) {
      var handle = handles[i];

      if (typeof handle !== 'function') {
        var type = toString.call(handle);
        var msg = 'Route.' + method + '() requires a callback function but got a ' + type
        throw new Error(msg);
      }

      debug('%s %o', method, this.path)

      var layer = Layer('/', {}, handle);
      layer.method = method;

      this.methods[method] = true;
      this.stack.push(layer); // 这个没弄明白
    }

    return this;
  };
});
```
<br/>
##### 第三部分

app.listen(port, () => console.log('Example app listening on port ${port}!'))
```javascript
app.listen = function listen() {
  var server = http.createServer(this);
  return server.listen.apply(server, arguments); // 这是什么写法？？？
};
```

---

##### 其他问题


1. express如何设置缓存 (好像课上讲过，看一下)
2. app.engine 设置模版引擎 jade, html 等
3. object.create、object.assign有什么区别
```javascript
var a = {'name': 'wyl', 'school': { 'grade': 1}}
var b = {'name': 'wyl', 'school': { 'grade': 2}}

Object.assign(a, b)
// 此时a.school.grade = 2

b.school.grade = 3

// 此a.school.grade = 3

// Object.assign 只会拷贝源对象自身的并且可枚举的属性到目标对象

```

```javascript
var a = {'name': 'wyl', 'school': { 'grade': 1}}
var b = Object.create(a)

// 指定b的原型对象是a, b.__proto__ 是a
```
<br/>

4.prototype 和__proto__区别

每个对象都有，隐式属性__proto__ 指向构造函数的原型prototype


5.Content-Type 请求媒体类型

6.Content-Disposition 设置如何显示文件

7.路由流程，express是如何识别的 （待看）