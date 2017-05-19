---
title: 实际开发中遇到的一些ffmpeg命令
date: 2015-10-28 15:00:00
tags: [Tools, FFmpeg]
---

试错很久，mark一下，Node.js 中可以使用fluent-ffmpeg


```PowerShell
ffmpeg -i video.mp4 -c copy -an video-no-audio.mp4 # 去掉video.mp4中的视频声音

ffmpeg -i video.mp4 -vn -acodec copy audio.aac # 拿到video.mp4中的声音

ffmpeg -i input -strict -2 output.wav # 将input音频转成wav

ffmpeg -i video-no-audio.mp4 -i 01.m4a -c:v copy -c:a copy merge-video-audio.mp4 # video-no-audio.mp4（没有声音的视频） 01.m4a（声音文件）合成新视频


ffmpeg -i video.mp4  (-ss 0 ) -t 5 -acodec copy -vcodec copy b.mp4 # 截取视频长度，从0到5秒


ffmpeg -ar 48000 -t 60(参数) -f s16le -acodec pcm_s16le -ac 2 -i /dev/zero -acodec copy output.wav #生成一个60秒的空白音频


ffmpeg -ar 48000 -t 5(参数) -f s16le -acodec pcm_s16le -ac 2 -i /dev/zero -acodec libmp3lame -aq 4 output.mp3 # 生成一个5秒的空白音频mp3


```