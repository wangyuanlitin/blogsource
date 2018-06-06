---
title: ES5 原生继承的实现方式
date: 2018-05-30 13:11:56
tags: JavaScript
---

主要通过babel将ES6代码转成ES5代码查看

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age
  } 
  getName () {
    return this.name
  }
}

var person = new Person('wyl', '11')
person.getName()

```

使用babel转成es5的代码

```javascript
'use strict';

var _createClass = function () {
  function defineProperties(target, props) {
    for (var i = 0; i < props.length; i++) {
      var descriptor = props[i];
      descriptor.enumerable = descriptor.enumerable || false;
      descriptor.configurable = true;
      if ("value" in descriptor)
        descriptor.writable = true;
        Object.defineProperty(target, descriptor.key, descriptor);
    }
  }
  return function (Constructor, protoProps, staticProps) {
    if (protoProps)
      defineProperties(Constructor.prototype, protoProps);
    if (staticProps)
      defineProperties(Constructor, staticProps);
    return Constructor;
  };
}();

function _classCallCheck(instance, Constructor) {
  if (!(instance instanceof Constructor)) {
    throw new TypeError("Cannot call a class as a function");
  }
}

var Person = function () {
  function Person(name, age) {
    _classCallCheck(this, Person);

    this.name = name;
    this.age = age;
  }

  _createClass(Person, [{
    key: 'getName',
    value: function getName() {
      return this.name;
    }
  }]);

  return Person;
}();

var person = new Person('wyl', '11');
person.getName();
```