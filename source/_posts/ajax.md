---
title: Ajax的核心 - XMLHttpRequest
date: 2018-02-08 11:34:44
tags: JavaScript
---

------

是什么？ 是一个异步JavaScript和XML，是一种**技术**
干什么？ 异步请求数据，快速呈现在界面上，不需要刷新页面

## 1. XMLHttpRequest
* **1.1** 简单的例子
同步
```javascript
var xhr = new XMLHttpRequest()
xhr.open('get', 'url', false)
xhr.send('数据') //　如果不需要发送数据，则必须传入null
//　因为是同步，接下来就可以从xhr读取返回内容
xhr.responseText // 返回结果
```

异步
```javascript
// 通过检测XHR对象的readyState属性，来判断当前的请求阶段
var xhr = new XMLHttpRequest()
xhr.open('请求类型post/get', URL, '是否是异步请求false/true')
xhr.send('数据') //　如果不需要发送数据，则必须传入null

xhr.onreadystatechange = function() {
  if(xhr.status... {
    ...
  }
}
```

* **1.2** 属性/方法

```javascript
let xhr = new XMLHttpRequest()
```
<!--more-->
| 方法        | 描述   |
| --------   | : -----  |
| open       | 初始化请求: xhr.open(method, url, async)<br> **注意:** 已经初始化过的请求，如果再调用open，会终止请求，相当于abort  |
| readyState | 不同状态：<br>0: 未初始化，尚未调用open()<br>1: 启动，已经调用open(), 还未调用send()<br>2: 发送，已经调用send()，但尚未接收到响应<br>3: 接收，已经接收到部分响应数据<br> |
| onreadystatechange     | 1. 用在异步请求<br>2. 必须正在调用open()之前指定onreadystatechange事件处理才能确保浏览器兼容性<br>3. readyState每更改一次都会触发一次 |
| response<br>responseText<br>responseType<br>responseXML | 返回结果 |
| status<br>statusText | 接口响应状态, status是状态码，statusText是状态码 + 原因短语 |
| upload | asdf |
| timeout| 请求在等待响应多少毫秒后终止 |
| ontimeout | 请求终止时会调用 |
<br>

| 方法      | 描述   |
| -------- | : -----  |
| open     | 初始化请求: xhr.open(method, url, async)<br> **注意:** 已经初始化过的请求，如果再调用open，会终止请求，相当于abort  |
| send     | 发送请求，只有一个参数 |
| setRequestHeader       | 设置请求头部信息，在open()方法之后，send()之前，(key, value)形式 |
| getResponseHeader       | 获取全部响应头 |
| getAllResponseHeaders       | 获取单个 ，比如：xhr.getResponseHeader('date') |
| abort     | 在接收到响应之前，终止请求，对xhr对象解除引用，（由于内存原因，不建议重用XHR对象） |


### * 注意：
> 1. Get请求 如果使用URL拼接参数时，为了防止错误，所有的名称和值都必须用encodeURIComponent()进行编码
> 2. 调用ontimeout处理程序的同时，如果onreadystatechange也触发了，此时在onreadystatechange内部访问xhr对象时，会导致错误


<br>
## 2. FormData
利用FormData对象来提交表单，需要将请求的编码类型(content-type)设置为multipart/form-data
[兼容性](https://caniuse.com/#search=FormData)

这是一个构造FormData最简单的例子
```javascript
let formdata = new FormData()
formdata.append('username', 'wxw')
formdata.apeend('password', 'wxw')

let xhr = new XMLHttpRequest()
xhr.open('get', 'url')
xhr.send(formdata)

```

如果要上传文件，怎么处理？

也是通过formdata.append()来添加，但是内容是File类型，或者是Blob类型

```javascript
// 上传一张图片,type根据实际情况，表示所含数据的MIME类型
let blob = new Blob(buffer, {type: 'png'/'jpg'/'jpeg'})
formdata.append('file', blob, filename) // filename如果不指定，使用默认文件名
```