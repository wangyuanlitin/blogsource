---
title: 列一些本周疑惑的问题
date: 2018-05-16 16:34:04
tags:
---

------

### 1、babel stage 有什么区别

对ES7草案的支持，stage-0、stage-1、stage-2、stage-3、stage-4所支持的插件不一样，stage-0包含了1、2、3的全部功能

### 2、 React元素和组件有什么区别
元素：最小部件，对象
```javascript
{
  type: '标签',
  key: '',
  props: {
    children: ''
  },
  ref: ''
}
```
<!--more-->

组件：由元素组成，是一个独立的、可复用的部件，有函数式组件和类组件

### 3、 为什么请求不在componentWillMount 这个生命周期
 页面阻塞，会出现长时间的空白

### 4、 state(状态)更新会被合并
```javascript
let counter = 1
this.setState({counter: counter + 1})
this.setState({counter: counter + 1})
this.setState({counter: counter + 1})
```
因为setState push到队列里面，一并更新的，上述代码counter并不会得到期望的值是4
```javascript
let counter = 1
this.setState((prevState, props) => ({
  counter: prevState.counter + 1
}));
this.setState((prevState, props) => ({
  counter: prevState.counter + 1
}));
this.setState((prevState, props) => ({
  counter: prevState.counter + 1
}));
```
### 5、 setState是怎么更新的
setState 的时候，react 会将要更新的值push到队列里面等待更新，所以不是即时的
### 6、 transform-class-properties
### 7、 preventDefault stopPropagation区别
stopPropagation　阻止事件冒泡，不在向document冒泡，但是默认事件还会执行
preventDefault　阻止默认事件，但是会发生冒泡
### 8、 createElement参数
```javascript
React.createElement(element, props, child)
```
### 9、 react 性能优化
### 10、 了解一下typescript
### 11、 状态提升
### 12、 受控组件和不受控组件
### 13、 重写生命周期shouldComponentUpdate，防止不必要的渲染
### 14、 Component， PureComponent
### 15、 浅比较，深拷贝实现

### 16、 突变对象

### 17、 https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/

### 18、 reconciliation算法

### 19、 Context

### 20、 web Component

### 21、 pm2  和 forever

### 22、 高阶组件

### 23、 javascript Number （伪）数轴

### 24、 TDD和BDD区别

### 25、 add(1, 2).should.equal(3)

### 26、 webhooks

### 27、 gitlab.ci

### 28、 看了哪些内容：
### 29、 mocha

### 30、 敏捷开发
### 31、 多人协同开发，如何拆分功能
### 32、 per workin 


### 33、 webpack生命周期


### 34、 css动画，有哪几种方式