---
title: Mocha的一些基本使用
date: 2018-01-25 14:52:19
tags: 测试
---

------

可以在Node.js环境和浏览器环境运行

### 1. 安装及运行
```javascript
npm install -g mocha || yarn global add mocha //　安装
mocha // 运行
```

### 2. 一个简单的测试脚本
<!--more-->
```javascript
const assert = require('assert')

describe('Test', function() {
  it ('1 == 1 ', function() {
    assert(1, 1)
  })
})
```

describe是一个模块，it是里面的测试用例，一个describe可以包含一个或者多个it块

### 3. 断言库
没有内置断言库，可以自己选择：例如：[should.js](https://github.com/shouldjs/should.js)、[expect.js](https://github.com/Automattic/expect.js)、[chai.js](http://chaijs.com/)、[better-assert](https://github.com/tj/better-assert)、[unexpected](http://unexpected.js.org/)

### 4. 一些用法

#### ４.1 asynchronous 异步
it回调中有一个callback，当测试执行完后，调用done()，用例就会结束
```javascript
describe('ASYNCHRONOUS', function() {
  it('should done after 1500ms', function(done) {
    setTimeout(() => {
      done()
    }, 1500);
  })
})
```

#### 4.2 ASYNC / AWAIT 同步
```javascript
function test() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('test')
    }, 1500)
  })
}

describe("test", function() {
  it('should valid', async function() {
    let value = await test()
    assert.equal(value, 'test')
  })
})
```
### 4.3 ARROW FUNCTIONS
不建议使用
原因：箭头函数内this的指向由上下文确定，在mocha内，使用箭头函数拿不到上下文，
但是如果内部没有this的话，就无所谓了
```javascript
// 第一种方式：箭头函数，会报错
describe('my suite', () => {
  it('my test', () => {
    this.timeout(1000);
    assert.ok(true);
  });
});
// 第二种方式：匿名函数，通过
describe('my suite', () => {
  it('my test', function(){
    // should set the timeout of this test to 1000 ms; instead will fail
    this.timeout(1000);
    assert.ok(true);
  });
});
```
### 4.4 HOOKS
mocha提供了四个钩子：before、after、beforeEach、afterEach
```javascript
describe('hooconstks', function() {
  before(function() { console.log('before') });

  after(function() { console.log('after')  });

  beforeEach(function() { console.log('beforeEach') }); // 执行在每个test实例之前, it之前

  afterEach(function() { console.log('afterEach') }); // 执行在每个test实例之后, it之后
  // ---------before---------
  describe('A', function(){
    it('A test1', function(){ assert.ok(1) })
    it('A test2', function(){ assert.ok(2) })
  })

  describe('B', function(){
    it('B test1', function(){ assert.ok(1) })
    it('B test2', function(){ assert.ok(2) })
  })
  // ---------after---------
});
```

### 5. 参数
--recursive 　test文件夹下有多层嵌套时
--reporter    运行mocha时，终端的一些展示
--timeout　　　默认设置2秒，超过2秒回报错timeout,　可以通过这个参数来设置最大时间
--no-timeouts 不设置timeout
　
### 6 MOCHA.OPTS
配置文件

### 7. 测试时的数据问题
场景: 当前测试的方法，内部依赖了别的方法，而且你也不需要测试依赖方法
就简单的写一下Sinon.js Stubs的用法，版本v4.2.2
* Stubs 替换某个调用行为

```javascript
let F = {
  getDate: function() {
    let date = new Date()
    return `${date.getFullYear()}-${date.getMonth()}-${date.getDate()} ${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`
  },
  toString: function () {
    return `今天是${this.getDate()}`
  }
}


describe('stub demo', function() {
  it('stub demo', function() {
    console.log(F.toString()) // 今天是2018-1-1 14:23:1(当前时间)

    let getDate = sinon.stub(F, 'getDate').callsFake(function(){
      return '2012-12-11 11:11:11'
    })

    console.log(F.toString()) // 今天是2012-12-11 11:11:11
    getDate.restore() // 重置stub
  })
})
```