---
title: Node.js Assert 模块
date: 2018-01-23 20:41:48
tags: [Node.js]
---


> 断言-主要用于Node.js测试

------
* API
  1. assert(value[, message])
  ```javascript
  const assert = require('assert')

  assert(1) // true
  assert(0) // false  报错信息: 0 == true
  assert(-1) // true

  assert(0, '报错报错报错') // false 报错信息：报错报错报错
  ```
  2. assert.ok(value[, message])
  ```javascript
  const assert = require('assert')

  assert.ok(1) // true
  assert.ok(0) // false 报错信息：0 == true
  assert.ok(0, '0报错了') // false 报错信息：0报错了
  ```
  <!--more-->
  3. assert.ifError(value)
  ```javascript
  // 如果value为真，throw error，应该和assert.ok()返回结果相反
  const assert = require('assert')

  assert.ifError(1) // false 报错信息：1

  assert.ifError('报错') // false 报错信息：报错
  ```
  4. assert.equal(actual, expected[, message])
  ```javascript
  // 使用==（Abstract Equality Comparison）进行比较，比较基本类型
  const assert = require('assert')
  const a = 1
  const b = '1'
  const c = 2

  assert.equal(a, b) // true
  assert.equal(a, c) // false 报错信息：1 == 2
  assert.equal(a, c, 'a不等于c') // false 报错信息：a不等于c

  ```
  5. assert.notEqual(actual, expected[, message])
  ```javascript
  // 和assert.equal()返回结果相反
  ```
  6. assert.strictEqual(actual, expected[, message])
  ```javascript
  const assert = require('assert')
  const a = 1
  const b = '1'

  assert.strictEqual(a, b) // false 报错信息：1 === '1'

  assert.strictEqual(a, b, '不全等') // false 报错信息：不全等
  ```
  7. assert.notStrictEqual(actual, expected[, message])
  ```javascript
  // 和assert.strictEqual()返回结果相反
  ```
  8. assert.deepEqual(actual, expected[, message])
  ```javascript
  // 使用==（Abstract Equality Comparison）进行比较
  const assert = require('assert')
  const obj1 = {a: {b: 1}}
  const obj2 = {a: {b: 1}}
  const obj3 = {a: {b: '1'}}
  const obj4 = {a: {b: 2}}

  assert.deepEqual(obj1, obj2) // true
  assert.deepEqual(obj1, obj3) // true
  assert.deepEqual(obj1, obj4) // false 报错信息：{ a: { b: 1 } } deepEqual { a: { b: 2 } }
  assert.deepEqual(obj1, obj4, 'obj1不等于obj4') // false 报错信息：obj1不等于obj4

  ```
  9. assert.notDeepEqual(actual, expected[, message])
  ```javascript
  // 两个值不相等时返回true，和assert.deepEqual()返回值正好相反
  ```
  10. assert.deepStrictEqual(actual, expected[, message])
  ```javascript
  // 使用===（Strict Equality Comparison）进行比较
  const assert = require('assert')
  const obj1 = {a: {b: 1}}
  const obj2 = {a: {b: 1}}
  const obj3 = {a: {b: '1'}}

  assert.deepStrictEqual(obj1, obj2) // true
  assert.deepStrictEqual(obj1, obj3) // false 报错信息：{ a: { b: 1 } } deepStrictEqual { a: { b: '1' } }
  assert.deepStrictEqual(obj1, obj3, 'obj1不等于obj3') // false 报错信息：obj1不等于obj3
  ```
  11. assert.notDeepStrictEqual(actual, expected[, message])
  ```javascript
  // 两个值不全等时返回true，和assert.deepStrictEqual()返回值正好相反
  ```
  12. assert.throws(block[, error][, message])
  13. assert.doesNotThrow(block[, error][, message])
  
  14. assert.fail([message])
  ```javascript
  // 可能就是专门用于报错的吧，想想不到使用的场景

  ```
  15. assert.fail(actual, expected[, message[, operator[, stackStartFunction]]])
  