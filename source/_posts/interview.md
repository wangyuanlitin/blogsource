---
title: 问题列表
date: 2018-05-29 19:18:24
tags: 前端
---

1. Array有哪些方法？
检测数组： isArray、
转换方法： toString、valueOf、toLocalString
栈方法： push、pop
队列方法：shift、unshift
重排序方法： sort、reverse
操作方法： concat、slice、splice
位置方法： indexOf
迭代方法： every、filter、forEach、map、some
缩小方法： reduce、reduceRight

sort是升序，比较的是字符串的大小
every、some的区别，every需要每项都满足条件，some需要部分满足，返回true/false

2. ES5基本类型、ES6基本类型
ES5基本类型：String、Number、Boolean、undefined、null
ES6基本类型：String、Number、Boolean、undefined、null、Symbol

Symbol 待补充
<!--more-->
3. null和undefined的区别
undefined是undefined类型，null 空对象指针是object类型
undefined已声明，未初始化
没有必要把一个值显示的设置为undefined，但是如果是一个未赋值的对象，就有必要设置成null

4. undefined、null是不是关键字
undefined （writable:false）是一个全局只读属性
undefined不是js的保留字，所以可以当作变量名在除了全局作用域以外的任何作用域中使用。

null是个关键字

5. Map、Set

6. typeOf 和 instanceOf
typeof function() {} === 'function'
返回值不一样：typeof返回具体类型，instanceof返回 true/false
typeof 一元运算符，返回值的类型，主要判断基本类型，引用类型返回的都是object
instanceof 判断引用类型，是否在链式上

7. new String() 和 直接定义var string = 'string' 有什么区别
类型不一样：一个是引用类型，一个是基本类型
存贮不一样：一个入堆，一个入栈

8. var、let、const之间的区别
let、const是块级作用域
var可以挂载到window上，let、const不可以
var可以声明同名变量，let、const不可以
var有变量提升，let、const没有

9. ES5有几种实现继承的方式

10. ES5 底层继承是怎么实现的

11. underScore.js 
是怎么判断为空的

12. 原型链

13. 闭包

14. Node.js 的全局属性

15. JQuery是怎么实现链式调用的