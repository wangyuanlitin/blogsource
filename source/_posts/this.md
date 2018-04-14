---
title: this关键字
date: 2018-04-08 17:14:10
tags: JavaScript
---

------
this在运行时绑定，取决于函数的调用方式

几种this绑定的情况

### 全局上下文

在全局执行上下文中this都指代全局对象，node 指向global，浏览器指向window

```javascript

var a = 'a'

console.log(window.a === a) // true

this.b = 'b'

console.log(window.b) // b

```

### 函数上下文
<!--more-->
在函数内部，this的值，取决与函数被调用的方式
简单调用
```javascript
function f1() {
  return this
}

f1() === window // 非严格模式
f1() === undefined // 严格模式

```
在严格模式下，this没有被执行的上下文，所以为undefined

### 箭头函数
箭头函数没有自己的this, 默认指向在定义它时所处的对象, 而不是执行时的对象

### 作为对象的方法
当函数作为对象的方法调用时，this指向调用函数的对象

```javascript
var obj = {
  value: 12,
  get: function() {
    return this.value
  }
}

obj.get() // 12
```

this 的绑定只受最靠近的成员引用的影响
```javascript
var obj = {
  value: 12,
  obj1: {
    value: 14,
    get: function() {
      return this.value
    }
  }
}
obj.obj1.get() // 14
```

### 原型链中的this
对于在对象原型链上某处定义的方法，同样的概念也适用。如果该方法存在于一个对象的原型链上，那么this指向的是调用这个方法的对象

```javascript
var obj = {
  f: function () {
    return this.a + this.b
  }
}

var obj1 = Object.create(obj)

obj1.a = 1
obj1.b = 4

obj1.f() // 5

```

### getter和setter中的this
this绑定到获取属性的对象上

### 作为构造函数
当函数用作构造函数是，this被绑定到正在构造的新对象

### 作为DOM事件处理函数
this指向触发事件的元素

### 作为内联事件处理函数
代码被on-event处理函数调用时，this指向监听器所在的DOM元素

### 修改this上下文

```javascript
var obj = {
  "a": "obj-a",
  "b": "obj-b"
}

var a = 'global-a'

function whatThis() {
  return this.a
}

whatThis() // global-a

```
当一个函数在其主体中使用 this 关键字时，可以通过使用函数继承自Function.prototype 的 call 或 apply 方法将 this 值绑定到调用中的特定对象。

### apply
```javascript
whatThis.call(obj) // obj-a
```

### call
```javascript
whatThis.apply(obj) // obj-a
```

使用 call 和 apply 函数的时候要注意，如果传递给 this 的值不是一个对象，JavaScript 会尝试使用内部 ToObject 操作将其转换为对象。
因此，如果传递的值是一个原始值比如 7 或 'foo'，那么就会使用相关构造函数将它转换为对象，所以原始值 7 会被转换为对象，像 new Number(7) 这样，而字符串 'foo' 转化成 new String('foo') 这样，例如：

### bind
创建一个与f具有相同函数体和作用域的函数，但是在这个新函数中，this将永久地被绑定到了bind的第一个参数，无论这个函数是如何被调用的。

```javascript
var obj = {
  "a": "obj-a",
  "b": "obj-b"
}

var obj1 = {
  "a": "obj-1"
}

var a = 'global-a'

function whatThis() {
  return this.a
}

var _whatThis = whatThis.bind(obj)

_whatThis() // obj-a
_whatThis() // obj-a
_whatThis() // obj-a

var _whatThis1 = _whatThis.bind(obj1) //bind只生效一次

_whatThis1() // obj-a
_whatThis1() // obj-a
_whatThis1() // obj-a
```