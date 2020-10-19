---
title: 小程序视频通话的问题总结
date: 2020-08-16 15:21:14
tags: [JavaScript, 小程序]
---

------

### 视频接入问题总结
> * 1、作为主播 live-pusher，需要获取摄像头和麦克风权限

可提前授权，用户拒绝的时候，可以做一些操作
** 一旦用户明确同意或拒绝过授权，其授权关系会记录在后台，直到用户主动删除小程序。

```javascript
wx.getSetting({
  success: (res) => {
    const { authSetting } = res;
    if (!authSetting['scope.camera']) {
       wx.authorize({
          scope: 'scope.camera',
          success: () => {
            resolve();
          },
       })
    }
  })
})
```

> * 2、主播接入，视频黑屏

获取权限的时，用户拒绝了，接入的时候，主播会黑屏；
看下控制台是否有其他报错报错，可以尝试重新接入；

> * 3、ios成功接入，安卓报一下错误

<img src='/assets/images/agora-error.png' style='width: 500px' />

先检查，引入的mini-app-sdk-production是否在本地又被打包或者压缩了一次；
如果还不可，尝试修改开发者工具本地设置，由少到多进行勾选，勾选「增强编译」

> * 4、小程序视频通话 安卓 905 connect socket failed

微信小程序目前最多支持 5 个 websocket，声网接入的时候会占用 1 个，先查看是不是超过了最大支持数目，如果没有可以先销毁声网socket，然后重新初始化加入频道

> * 5、在通话过程中，远端视频突然黑屏

检查用户拉流地址是不是改变了，但是没有更新

```html
<live-player bindstatechange="" binderror="" ></live-player>
```

捕获bindstatechange, binderror 返回的状态，是否有错误

> * 6、网络波动

网络轻微抖动，websocket还未断开，对视频通话基本没有影响
网络大抖动，并且推流失败，尝试重新加入频道

> * 7、部分手机接入视频的时候，使用的是4G网络，流量消耗大

调用微信API，wx.getNetworkType() ，获取当前网络类型，根据网络类型调整live-pusher推流分辨率、视频码率、音频音质
