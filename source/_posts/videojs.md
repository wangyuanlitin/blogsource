---
layout: false
title: videojs
date: 2017-09-23 15:01:59
tags: [HTML5，javascript, 前端]
---

<html>

<head>
    <link href="http://vjs.zencdn.net/6.2.7/video-js.css" rel="stylesheet">
    <script src="http://vjs.zencdn.net/6.2.7/video.js"></script>
    <!-- <script src="jquery-2.0.0.min.js"></script> -->
    <style type="text/css">
    .video-js .vjs-time-control {
        display: block;
    }
    </style>
</head>

<body>
    <video id="my-player" class="video-js vjs-default-skin" controls preload="auto" width="640" height="268">
        <source src="/assets/video/oceans.mp4" type='video/mp4'>
    </video>
    <script type="text/javascript">
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
        "autoplay": true,
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

    }, function() {
        $(".vjs-control-bar").append('<div class="logo" style="text-align: center;"><img src="logo.png" style="height: 80%; margin: 5% 0;"/></div>');
        console.log("done")
    });
    $("#my-player").on("keydown", function(e) {
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
    </script>
</body>

</html>