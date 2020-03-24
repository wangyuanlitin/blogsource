---
title: Charles 抓包工具搭建
date: 2019-06-12 16:18:32
tags: 
---

------
场景：小程序webview联调，网页拿不到webview传过去的参数，页面访问没有nginx日志，无法定位问题，尝试是否可以通过抓包工具获取访问链接

### 1. 安装
官网下载走一波


### 2. 网站配置
2.1 打开以后的界面
![question](/assets/images/cls-01.png)

<!--more-->

2.2 按照图示打开macos proxy后
![question](/assets/images/cls-02.png)
2.3 用safari随意访问联网的链接，就会看到下面的界面
![question](/assets/images/cls-03.png)


到此为止，网页的抓包就完成设置

### 3. iphone 抓包配置
3.1 打开proxy setting
![question](/assets/images/cls-04.png)
![question](/assets/images/cls-05.png)

3.2 安装手机端证书，为了可以访问https，如果不安证书，无法看到具体https请求，会显示unkown

![question](/assets/images/cls-06.png)
![question](/assets/images/cls-07.png)

根据上述提示设置手机代理

注意： 要保证手机和电脑在同一个网段内，（不在一个网段无法打开安装证书页面）
解决办法：iphone连接手机分享的热点，再设置

3.3 手机端设置

<img src="/assets/images/cls-08.jpeg" style="width: 500px" />
配置代理
<img src="/assets/images/cls-09.jpeg" style="width: 500px"/>
代理服务器，地址不明白，可以查看3.2第二张截图
<img src="/assets/images/cls-10.jpeg" style="width: 500px" />

完成以后，在safari里面打开chls.pro/ssl，如果提示打不开，检查手机和电脑是否在同一网段
打开会看到，点击“允许”，允许后会提示，到设置里面找“描述文件”
<img src="/assets/images/cls-11.jpeg" style="width: 500px" />
打开手机 设置 -> 通用 -> 描述文件，下载安装证书
<img src="/assets/images/cls-12.jpeg" style="width: 500px" />
安装完成后，打开设置 -> 通用 -> 关于本机 -> 证书信任设置， 将charles设置为信任
<img src="/assets/images/cls-12.jpeg" style="width: 500px" />

全部完成，接下来就可以通过电脑端，查看手机端的访问记录