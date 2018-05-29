---
title: 列一些本周疑惑的问题
date: 2018-05-16 16:34:04
tags:
---

1、babel stage 有什么区别
对ES7草案的支持，stage-0、stage-1、stage-2、stage-3、stage-4所支持的插件不一样，stage-0包含了1、2、3的全部功能

2、 React元素和组件有什么区别
元素：最小部件，对象
{
  type: '标签',
  key: '',
  props: {
    children: ''
  },
  ref: ''
}

组件：由元素组成，是一个独立的、可复用的部件，有函数式组件和类组件

3、 为什么请求不在componentWillMount 这个生命周期
 页面阻塞，会出现长时间的空白

4、 state是在什么情况下创建的

5、 state(状态)更新会被合并
6、 setState是怎么更新的
setState 的时候，react 会将要更新的值push到队列里面等待更新，所以不是即时的
6、 transform-class-properties
7、 preventDefault stopPropagation区别
stopPropagation　阻止事件冒泡，不在向document冒泡，但是默认事件还会执行
preventDefault　阻止默认事件，但是会发生冒泡
8、 createElement参数
9、 react 性能优化
10、 setState() 合并
11、 了解一下typescript
12、 状态提升
13、 受控组件和不受控组件
14、 重写生命周期shouldComponentUpdate，防止不必要的渲染
15、 Component， PureComponent
16、 浅比较，深拷贝实现

突变对象

https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/

reconciliation算法

Context

web Component

pm2  和 forever

高阶组件

javascript Number （伪）数轴

TDD和BDD区别

add(1, 2).should.equal(3)

webhooks

gitlab.ci




看了哪些内容：
mocha

敏捷开发
多人协同开发，如何拆分功能
per workin 


2. webpack生命周期


css动画，有哪几种方式