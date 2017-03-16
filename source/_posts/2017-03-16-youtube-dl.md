---
title: youtube 视频下载工具
date: 2017-03-16 14:54:34
tags: [youtube,youtube-dl]

---

这里介绍一个比较好用的视频下载命令行工具: [youtube-dl](https://github.com/rg3/youtube-dl) , 可以批量下载youtube(以及其他视频网站)上的视频

<!-- more -->

## 特点
- 由于工具本身是 python 程序, 有良好的跨平台性
- 可以批量下载youtube 用户或者频道 的视频
- 可以选择视频/音频质量, 如果原视频有4k也可以下载
- 由于 youtube 上高分辨率的视频一般是 视频/音频 文件单独分开的, 这个工具还可以在下载音视频之后自动合并成mkv(需要安装 ffmpeg, 并保证路径中可以检查到 ffmpeg 程序)
- 可以用配置文件来设定常用配置

## 安装
*nix 系统

```sh
sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
```

win 系统可以去项目页下载 exe 程序

## 使用
详细说明在项目页有, 这里说一下简单的用法

```sh
    # --proxy 127.0.0.1:8087 使用代理
    # --no-check-certificate 禁止证书认证, 开启认证部分代理会不能用
    # -f bestvideo+bestaudio 下载最好的 视频+音频, 并且回自动合并为mkv(需要安装 ffmpeg)
    youtube-dl --proxy 127.0.0.1:8087 --no-check-certificate -f bestvideo+bestaudio https://www.youtube.com/watch?v=xxxxxxx


    # --playlist-items 可以指定要下载的视频的索引, 比如 2-8 就是 第2到第8个视频(最新的一个是1)
    # --reject-title 可以指定一个regexp或字符串来排除匹配到的视频, 可以和上面的选项配合使用!
    youtube-dl --playlist-items 2-8 --reject-title FOO https://www.youtube.com/channel/xxxxxxxxx/videos
```

## 使用配置文件
可以把常用的选项放在配置文件里面, 这样运行命令会方便很多
配置文件路径在 ~/.config/youtube-dl/config
```sh
    --no-check-certificate

    -f bestvideo+bestaudio/best

    # Use this proxy
    --proxy 127.0.0.1:8087

    # Save all videos under Movies directory in your home directory
    -o ~/video/%(title)s.%(ext)s
```
