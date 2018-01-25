---
title: Mocha测试框架 
date: 2018-01-25 14:52:19
tags:
---

------

读 /'moʊkə/，可以在Node.js环境和浏览器环境运行

### 1. 安装
```shell
npm install -g mocha 
```
或者是
```shell
yarn global add mocha
```

### 2. 运行
需要当前目录有test文件夹或者是test.js文件
```shell
mocha
```
如果test文件夹下有多级目录是
```shell
mocha --recursive
```

### 3. 一个简单的测试脚本
```javascript
describe('Test', function() {
  it ('1 == 1 ', function() {
    assert(1, 1)
  })
})
```

describe 是test suite，it是test cate，一个describe可以包含一个或者多个it块

### 4. 断言库
可以依自己的喜好选择
例如：[should.js](https://github.com/shouldjs/should.js)、[expect.js](https://github.com/Automattic/expect.js)、[chai.js](http://chaijs.com/)、[better-assert](https://github.com/tj/better-assert)、[unexpected](http://unexpected.js.org/)

### 5. 基本用法

#### 5.1 asynchronous 异步
it回调中有一个callback，当测试执行完后，调用done()，用例就会结束
```javascript
describe('User', function() {
  describe('#save()', function() {
    it('should save without error', function(done) {
      var user = new User('Luna');
      user.save(done);
    });
  });
});
```

#### 5.2 ASYNC / AWAIT
```javascript
beforeEach(async function() {
  await db.clear();
  await db.save([tobi, loki, jane]);
});

describe('#find()', function() {
  it('responds with matching records', async function() {
    const users = await db.find({ type: 'User' });
    users.should.have.length(3);
  });
});
```
#### 5.3 HOOKS
```javasript
describe('hooks', function() {
  before(function() {
    // runs before all tests in this block
  });

  after(function() {
    // runs after all tests in this block
  });

  beforeEach(function() {
    // runs before each test in this block
  });

  afterEach(function() {
    // runs after each test in this block
  });

  // test cases
});
```
#### 5.4 DESCRIBING HOOKS
```javascript
beforeEach(function() {
  // beforeEach hook
});

beforeEach(function namedFun() {
  // beforeEach:namedFun
});

beforeEach('some description', function() {
  // beforeEach:some description
});
```