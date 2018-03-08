---
title: Video.js ControlBar设置代码片段
date: 2018-02-02 11:54:59
tags: [JavaScript, 代码片段]
---

------

```javascript
  videojs.getComponent('ControlBar').prototype.options_ = {
    children: [
      'playToggle',
      'progressControl',
      'currentTimeDisplay',
      'timeDivider',
      'durationDisplay',
      'volumeMenuButton',
      'PlaybackRateMenuButton',
      'fullscreenToggle'
    ]
  }
  var player = videojs(document.getElementById("my-player"), {
    "autoplay": false,
    "controls": true,
    "playbackRates": [0.5, 1, 1.5, 2],
    "controlBar": {
        'playToggle': true, //　播放暂停按钮
        'volumeMenuButton': { 'inline': false },
        'timeDivider': true,
        'durationDisplay': true, //总共多上时间
        'currentTimeDisplay': true,
        'fullscreenToggle': true //全屏
    },
  }, function () {
    $(".vjs-control-bar").append('<div class="logo" style="text-align: center;"><img src="/assets/images/me.jpeg" style="height: 80%; margin: 5% 0;"/></div>');
  });
  $("#my-player").on("keydown", function (e) {
    var keyCode = e.keyCode;
    if (keyCode === 39) {
      //快进
      player.currentTime(player.currentTime() + 5)
    } else if (keyCode === 37) {
      //后退
      player.currentTime(player.currentTime() - 5)
    } else if (keyCode === 32) {
      if (player.paused()) {
        player.play();
      } else {
        player.pause();
      }
    }
  })
```