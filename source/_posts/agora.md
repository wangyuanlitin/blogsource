---
title: 基于声网的小程序直播互动
date: 2020-08-16 15:21:14
tags: [JavaScript, 小程序]
---

------

### 一、小程序原生直播组件
在小程序中使用直播业务，需要使用小程序的原生媒体组件
1. live-pusher
> 实时音视频录制，需要授权scope.camera、scope.record

主要参数：
url 推流地址，目前仅支持 rtmp 格式
mode 模式 RTC（实时通话）
2. live-player
> 实时音视频播放

src 播放音视频地址
3. 简单的小实现
前端小程序代码
<!--more-->
```
// index.wxml
<view class="container">
  <live-pusher
    mode="RTC"
    autopush
    url="{{pushUrl}}"
  ></live-pusher>
  <live-player
    mode="RTC"
    autoplay="{{true}}"
    src="{{pullUrl}}"
  ></live-player>
</view>

// index.js
const app = getApp()

Page({
  data: {
    pushUrl: "",
    pullUrl: "",
    pullStreamName: "stream1",
    pushStreamName: "stream1",
  },
  onReady: function () {
    this.setData({
      pushUrl: `rtmp://192.168.2.1:1935/live/${this.data.pushStreamName}`,
      pullUrl: `rtmp://192.168.2.1:1935/live/${this.data.pullStreamName}`
    })
  }
})
```
后台可以使用node-media-server搭建本地的rtmp服务

小程序端可以在开发工具直接预览
> 注意：手机端预览的时候，网络要和本地搭建的rtmp服务在同一局域网内

### 2、 声网
可以实现的功能
音视频通话
音视频直播
使用场景：

一对一：线上课堂、互联网医院、高级客服、视频认证

一对多：一个直播其他人观看，上课

多对多：巡场、连麦

### 3、 项目中使用
### 4、 遇到的问题
* 接入不了声网，接入声网慢
* 小程序ws建立多个
* 视频过程中，屏幕黑屏
* 中途退出，再进入