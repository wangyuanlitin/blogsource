---
title: JavaScript中的getter和setter
date: 2018-03-07 20:30:29
tags: JavaScript
---

------

get和set访问器分别是用来获取或者设置对象属性的

### 1. 浏览器支持

（1）.IE9+
（2）.Edge
（3）.Chrome
（4）.Firefox
（5）.Opera
（6）.Safari

### 2. 标准get和set访问器的使用
<!--more-->
```javascript
var Field = {
  value: 100,
  get val() {
    console.log('getter')
    return this.value
  },
  set val(value) {
    console.log('setter')
    this.value = value
  }
}

Field.val          // 输出getter 100
Field.val = 1001   // 输出setter 1001
Field.val          // 输出getter 1001
```

### 3. 模拟实现get和set访问器
```javascript
var Field = {
  value: 100,
  getValue: function () {
    return this.value
  },
  setValue: function (value) {
    this.value = value
  }
}

Field.getValue()     // 输出100
Field.setValue(1001) // 输出 1001
Field.getValue()     // 输出 1001
```

### 4. 使用Object.defineProperty()方法实现get和set访问器功能
```javascript
var Field = {
  value: 100
}

Object.defineProperty(Field, '_value', {
  get: function () {
    return this.value
  },
  set: function (value) {
    this.value = value
  }
})

Field.value         // 输出100
Field._value = 1001 // 输出100
Field.value         // 输出100
```

写到这里，其实我并没有发现get和set的优势，和类方法差不多，只不过它们是类属性
唯一能想到的就是组合属性这种场景，类似：
```javascript
var Stu = {
  firstName: 'YL',
  lastName: 'W',
  get fullName () {
    return this.firstName + '.' + this.lastName
  }
}

Stu.fullName    // 输出 YL.W
```
