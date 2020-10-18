---
title: 小程序视频通话的问题总结
date: 2020-08-16 15:21:14
tags: [JavaScript, 小程序]
---

------

实现音视频通话，会用到小程序原生的两个媒体组件，live-pusher(实时音视频录制)和live-play(实时音视频播放)，使用这两个组件，需要先通过类目审核，再在小程序管理后台，「开发」-「接口设置」中自助开通该组件权限，具体开通可以看一下官方文档。

小程序官方文档里面参数都有详细的解释，这里只列一下在过程中会遇到的问题

### 一、简单的小实现

搭建了一个简单推流拉流Demo，主要是熟悉一下流程，然后熟悉一下原生的参数设置。
后台使用node-media-server搭建本地rtmp服务，小程序端使用live-pusher进行推流，通过后台的协议转发，在pc端获取到推流地址后，可以进行实时播放

<!-- [Demo地址](https://git.zhonganinfo.com/za-wangyuanli/wechat-pusher-player) ：https://git.zhonganinfo.com/za-wangyuanli/wechat-pusher-player -->

### 二、声网接入
```javascript
// 流程-伪代码
const AgoraMiniappSDK = require("mini-app-sdk-production.js"); // 声网SDK，从官网下载

const channel = ''; // 房间号
const uid = ''; // 用户id

const APPID = ''; // 声网的APPID

Page({
  data: {
    media: [],
  },

  onReady: function () {
    this.initAgoraChannel(uid, channel)
      .then(url => {
        this.addMedia({
          mediaType: '',
          uid
          url
        })
      })
  },

  /**
   * addMedia 将流地址更新到media里面
   * 区分一下是推流、还是拉流
   * 推流地址要用live-pusher渲染，拉流地址要live-player渲染
  */
  addMedia({mediaType, uid, url}) {
    let media = this.data.media || [];

    if (isBroadcaster()) {
      // pusher
      media.splice(0, 0, {
        mediaType: mediaType,
        uid: `${uid}`,
        url: url,
      });
    } else {
      // player
      media.push({
        type: mediaType,
        uid: `${uid}`,
        url: url,
      });
    }
    this.setData({
      media
    })
  },

  /**
   * 创建对象 -> 监听 -> 设置角色 -> 加入房间 -> 主播 ？推流 ：''
  */

  initAgoraChannel: function (uid, channel) {
    return new Promise((resolve, reject) => {
      client = new AgoraMiniappSDK.Client();

      // 监听
      client.on("stream-added", e => {
        let uid = e.uid;
        client.subscribe(uid, (url) => {
          console.log(`用户：${uid} 进入了房间，拉流地址是${url}`);
        });
      });

      client.on("stream-removed", e => {
        let uid = e.uid;
        console.log(`用户：${uid} 离开了房间`);
      });

      client.on("error", err => {
        let errObj = err || {};
        let reason = errObj.reason || "";
        console.log(`client 发生了错误，原因: ${reason}`);
      });

      client.on('update-url', e => {
        let uid = e.uid;
        let url = e.url;
        console.log(`用户：${uid}的拉流地址更新为${url}`)
      });

      // 以上
      
      client.setRole('broadcaster');
      client.init(APPID);
      client.join(token, channel, uid);

      if (isBroadcaster()) {
        client.publish(url => {
          resolve(url);
        })
      }
    });
  },

  /**
   * 重新加入频道，流程和初始化频道一致
   * 
   * 方法client.join() ----> client.rejoin()
   * client.destory()
  */
  rejoinAgoraChannel: function (uid, channel) {
    return new Promise((resolve, reject) => {
      client = new AgoraMiniappSDK.Client();

      // 监听
      client.on("stream-added", e => {
        let uid = e.uid;
        client.subscribe(uid, (url) => {
          console.log(`用户：${uid} 进入了房间，拉流地址是${url}`);
        });
      });

      client.on("stream-removed", e => {
        let uid = e.uid;
        console.log(`用户：${uid} 离开了房间`);
      });

      client.on("error", err => {
        let errObj = err || {};
        let reason = errObj.reason || "";
        console.log(`client 发生了错误，原因: ${reason}`);
      });

      client.on('update-url', e => {
        let uid = e.uid;
        let url = e.url;
        console.log(`用户：${uid}的拉流地址更新为${url}`)
      });

      // 以上
      
      client.setRole('broadcaster');
      client.init(APPID);
      client.rejoin(token, channel, uid);

      if (isBroadcaster()) {
        client.publish(url => {
          resolve(url);
        })
      }
    });
  }
})
```

上面是一个简单的流程伪代码，

<!-- [详细代码](https://git.zhonganinfo.com/za-wangyuanli/agora)：https://git.zhonganinfo.com/za-wangyuanli/agora -->


### 三、视频接入问题总结
> * 1、作为主播 live-pusher，需要获取摄像头和麦克风权限

可提前授权，用户拒绝的时候，可以做一些操作
** 一旦用户明确同意或拒绝过授权，其授权关系会记录在后台，直到用户主动删除小程序。

```javascript
  // 获取麦克风权限
  getRecordAuth(authSetting) {
    return new Promise((resolve, reject) => {
      if (!authSetting['scope.record']) {
        Taro.authorize({
          scope: 'scope.record',
          success: () => {
            resolve();
          },
          fail: (e) => {
            console.log('用户本次拒绝了麦克风权限获取')
            reject(e);
          },
        });
      } else {
        console.log('用户之前拒绝了麦克风权限获取');
        resolve();
      }
    });
  }

  // 获取摄像头权限
  getCameraAuth(authSetting) {
    return new Promise((resolve, reject) => {
      if (!authSetting['scope.camera']) {
        console.log('需要获取摄像头权限');
        Taro.authorize({
          scope: 'scope.camera',
          success: () => {
            resolve();
          },
          fail: (e) => {
            console.log('用户本次拒绝了摄像头权限获取')
            reject(e);
          },
        });
      } else {
        console.log('用户之前拒绝了摄像头权限获取')
        resolve();
      }
    });
  }

  getAuthority() {
    return new Promise((resolve, reject) => {
      Taro.getSetting({
        success: (res) => {
          const { authSetting } = res;
          console.log(authSetting);
          this.getRecordAuth(authSetting)
            .then(() => {
              return this.getCameraAuth(authSetting);
            }).then(() => {
              resolve();
            }).catch((e) => {
              reject(e);
            });
        },
      });
    });
  }

  getAuthority();
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

```javascript
  client.on('update-url', e => {
    let uid = e.uid;
    let url = e.url;
    console.log(`用户：${uid}的拉流地址更新为${url}`)
  });
```

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
