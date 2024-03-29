---
title: 问题列表
date: 2018-05-29 19:18:24
tags: JavaScript
---

------

### 1. Array有哪些方法？
> 检测数组： isArray、
> 转换方法： toString、valueOf、toLocalString
> 栈方法： push、pop
> 队列方法：shift、unshift
> 重排序方法： sort、reverse
> 操作方法： concat、slice、splice
> 位置方法： indexOf
> 迭代方法： every、filter、forEach、map、some
> 缩小方法： reduce、reduceRight

其中sort是升序，比较的是字符串的大小，所以 [1, 2, 10].sort()， 返回的结果是 [1, 10, 2]， 这不是期望的
<!--more-->
正确是使用方式：
```javascript
// 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值
// 若 a 等于 b，则返回 0
// 若 a 大于 b，则返回一个大于 0 的值
[1, 2, 10].sort(function(a, b) {
  return a - b // 升序
})
```
every、some的区别，every需要每项都满足条件，some需要部分满足，返回true/false
filter、map 返回一个新的数组
slice 和 splice的区别：slice返回选定数组；　splice删除元素，并向数组中添加新的元素
reduce 用来做什么
### 2. ES5基本类型、ES6基本类型
> ES5基本类型：String、Number、Boolean、undefined、null
> ES6基本类型：String、Number、Boolean、undefined、null、Symbol

Symbol 待补充
### 3. null和undefined的区别
> 类型不一样：undefined是undefined类型，null 空对象指针是object类型
> undefined已声明，未初始化
> 没有必要把一个值显示的设置为undefined，但是如果是一个未赋值的对象，就有必要设置成null

### 4. undefined、null是不是关键字
> undefined （writable:false）是一个全局只读属性
> undefined不是js的保留字，所以可以当作变量名在除了全局作用域以外的任何作用域中使用。

> null是个关键字

### 5. Map、Set

### 6. typeOf 和 instanceOf
> typeof function() {} === 'function'
> 返回值不一样：typeof返回具体类型，instanceof返回 true/false
> typeof 一元运算符，返回值的类型，主要判断基本类型，引用类型返回的都是object
> instanceof 判断引用类型，是否在链式上

### 7. new String() 和 直接定义var string = 'string' 有什么区别
> 类型不一样：一个是引用类型，一个是基本类型 typeof
> 存贮不一样：一个入堆，一个入栈

### 8. var、let、const之间的区别
> let、const是块级作用域
> var可以挂载到window上，let、const不可以
> var可以声明同名变量，let、const不可以
> var有变量提升，let、const没有

### 9. ES5有几种实现继承的方式
原型链继承 propotype

### 10. ES5 底层继承是怎么实现的
Object.defineProperty()
### 11. underScore.js 
是怎么判断为空的

### 12. 原型链
每个对象都有一个__proto__隐

### 13. 闭包

### 14. Node.js 的全局属性
> global
> process
> console
> __filename 当前执行脚本/文件所在目录+文件名   
> __dirname 当前执行脚本/文件所在目录
> setTimeout/setInterval
> clearTimeout/clearInterval

### 15. JQuery是怎么实现链式调用的

### 16. Http状态码

> 1xx 信息 100 需要继续请求/101 协议切换
> 2xx 成功请求 200 正常请求/204 没有内容
> 3xx 重定向 301 永久移除/302 临时移除 /304 Not modified
> 4xx 客户端错误 401 授权失败/403 Forbidden/404 没有资源
> 5xx 服务端错误 500 服务端报错/502 网关错误/504 超时

### 17. HTTP和HTTPS的区别
HTTPS加密 HTTP是明文传输
HTTP是80端口 HTTPS是443端口

### 18. HTTP1.0、HTTP1.1、HTTP2.0的区别

### 19. __proto__ 和 prototype的区别
所有的对象都有__proto__
只有函数有prototype

### 20. input和textarea之间的区别
input是一个多行输入框

### 21. new 做了什么事情
```javascript
var person = new Person('wyl', '11')

// new 做的事情就是将person的__proto__属性指向Person.prototype
```
这些问题其实是面试问题列表