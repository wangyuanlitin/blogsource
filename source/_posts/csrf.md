---
title: 跨站点请求伪造（CSRF）
date: 2018-05-05 10:28:36
tags: Web安全
---

------

利用用户身份操作用户账户，注入额外网络请求的一种攻击方式

### 原理
用户访问并登录可信任网站A
验证通过后，产生A网站的Cookie
在没有退出登录的情况下，继续访问B网站
B要求访问A网站并发出一个请求，这是B就拿到了A网站的Cookie
B得到权限后就可以模拟用户操作了，可以想A服务器去发起数据请求，做一些操作

发生的原因是，网站是通过cookie识别用户的，只要不关闭浏览器或者退出登录，那访问网站是都会带上cookie

### 进阶例子
#### 浏览器的cookie策略
浏览器Cookie分为两种：
>* session cookie：浏览器关闭后失效，保存在内存中
>* Third-party Cookie：服务器在set-cookie时指定了Expire时间，只有过期时间到了才会失效，保存在本地

<!--more-->
例子：
1. 访问www.a.com时，浏览器会写入两个Cookie，Session Cookie和Third-party Cookie， 写入成功后，访问同域不同页面时，发现cookie被发送
2. 在未退出登录的情况下，访问www.b.com构造的攻击页面iframe src='http://www.a.com', 这时候只发送了Session Cookie，Third-party Cookie被禁止

这是处于安全考虑，IE默认禁止了浏览器在img、iframe、script、link等标签中发送第三方Cookie

当前主流浏览器 默认会拦截Third-party Cookie，ie7～8 safari
不会拦截 Fixfox2～3, opera chrome andriod

如果csrf攻击不表并不需要Cookie，也不用考虑浏览器的Cookie策略了

### 百度CSRF Worm

如何产生：
暴露了两个接口：
http://xxxx?sn=用户账户&co=消息内容  // 通过修改sn、co，可以通过链接给指定用户发送消息
http://xxxx?un=用户账户 // 通过修改un，可以查询用户好友

两者结合起来，就可以组成一个CSRF Worm-让一个用户查看到恶意页面后，将给他所有的好友发送一条短消息，然后短消息中包含一张图片，地址指向CSRF页面，使得这些好友再次将消息发送给他们的好友，使Worm得以传播


### 危害
1. 隐私泄漏
2. 数据操作

### 防御
1. 验证码
好处：无法构造验证码
弊端：不可能每个操作都加验证码

2. Referer Check 
好处：检测Referer值是不是在指定页面
弊端：服务器并非什么时候都能取到referer

3. Token
好处：csrf本质，重要的参数可以被攻击者猜到，参数有加密的token可以有效抵御攻击
弊端：需要手动加，同时token的安全难以保证