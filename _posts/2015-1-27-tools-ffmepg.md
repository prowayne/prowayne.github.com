--- 
title: ffmepg-极简单的媒体工具
layout: post
category: tools
---

## 简介
A complete, cross-platform solution to record, convert and stream audio and video. -- [FFmepg][1]  

## 几个小例子
从此视频音频的转换,处理变得相当简单.

1. 视频转码  
`ffmpeg -i input.mp4 output.avi`

2. 从视频导出图片(1pic/sec)
`ffmpeg -i input.avi -r 1 -s WxH -f image2 out-%03d.jpeg`

3. 从图片生成视频
`ffmpeg -f image2 -i in-%03d.jpeg -r 12 -s WxH out.avi`

4. 从视频提取音频
`ffmpeg -i source.mp4 -ab 128k dest.mp3`

## 总结
ffmepg 拥有极多的参数,基本覆盖了视频处理的各个方面, 开放了很多的接口, 所以能很方便的集成到自己的应用中.在很多流行的视频播放器中得到应用, 如QQ影音, 暴风影音等.  
注意: ffmepg遵循GPL开源协议.

[1]:http://ffmpeg.org/ "官网"