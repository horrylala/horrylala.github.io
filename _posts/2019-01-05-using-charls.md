---
layout:     post
title:      "charles抓包技巧"
subtitle:   " \"调试神器\""
date:       2019-01-05 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - 调试
    - 抓包
    - http
---

# charles抓包技巧

* 1.共享一个手机wifi(命名为honor-wifi)
* 2.电脑连接wifi(ip地址为：192.168.43.248)，手机连接同一个wifi(honor-wifi),并且设置
HTTP代理 -> 手动 -> 服务器为192.168.43.248(电脑的ip地址)，端口号为charles设置的端口号(8888)
* 3.proxy -> ssl setting -> 勾选Enable SSL Proxying，add *.443
* 4.Proxy -> proxy setting, port选择8888，勾选下面的enable transparent HTTP proxying
* 5.安装电脑证书。
电脑上，Help -> ssl proxying -> install root certificat，设置权限运行
* 6.安装手机证书。
浏览器上输入chrls.pro/ssl，然后安装证书。
* 7.手机上，通用 -> 关于手机 -> 证书信任设置，打开charls那个按钮


You may need to configure your browser or application to trust the Charles Root Certificate. See SSL Proxying in the Help menu.