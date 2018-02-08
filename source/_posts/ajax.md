---
title: Ajax的核心 - XMLHttpRequest
date: 2018-02-08 11:34:44
tags: javascript
---

------

是什么？ 是一个异步JavaScript和XML
干什么？ 异步请求数据，快速呈现在界面上，不需要刷新页面

## 1. 核心 - XMLHttpRequest
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

| 方法        | 描述   |
| --------   | : -----  |
| open       | 初始化请求: xhr.open(method, url, async)<br> **注意:** 已经初始化过的请求，如果再调用open，会终止请求，相当于abort  |
| onreadystatechange     | \$1600 |
| readyState     | \$1600 |
| response     | \$1600 |
| responseText     | \$1600 |
| responseType     | \$1600 |
| responseXML     | \$1600 |
| status     | \$1600 |
| statusText     | \$1600 |
| upload     | \$1600 |
<br>

| 方法        | 描述   |
| --------   | : -----  |
| open       | 初始化请求: xhr.open(method, url, async)<br> **注意:** 已经初始化过的请求，如果再调用open，会终止请求，相当于abort  |
| send       | \$1600 |
| setRequestHeader       | \$1600 |
| getResponseHeader       | \$1600 |
| getAllResponseHeaders       | \$1600 |
| abort     | \$1600 |


* **1.3** 方法介绍




必须正在调用open()之前指定onreadystatechange事件处理才能确保浏览器兼容性
xhr的readyState每变化一次，就会触发一次onreadystatechange
xhr的readyState不同状态：
0: 未初始化，尚未调用open()
1: 启动，已经调用open(), 还未调用send()
2: 发送，已经调用send()，但尚未接收到响应
3: 接收，已经接收到部分响应数据
4: 完成，已经接收到全部响应数据

在接收到响应之前，还可以调用abort()来取消异步，取消后xhr对象会停止触发事件

XHR对象提供的两种头部(请求头，响应头)
请求头部
Accept: 浏览器能够处理的内容类型
Accept-Charset: 浏览器能够显示的字符集
Accept-Encoding: 浏览器能够处理的压缩编码
Accept-Language: 浏览器当前设置的语言
Connection： 浏览器和服务器之间连接的类型
Cookie：当前页面Cookie
Host：发出请求的页面所在的域
Refere：发出请求的页面的URL
User-Agent：浏览器用户代理字符串

XHR设置请求头
在open()方法之后，send()之前

xhr.setRequestHeader()

响应头部
xhr.getAllResponseHeaders() // 获取全部响应头
xhr.getResponseHeader() // 获取单个 ，比如：xhr.getResponseHeader('date')

### Get 获取数据
将参数拼接到URL上时，为了防止出现错误，所有的名称和值都必须用encodeURIComponent()进行编码

### Post

### FormData

### 超时
xhr.timeout = 1000
xhr.ontimeout = function () {

}