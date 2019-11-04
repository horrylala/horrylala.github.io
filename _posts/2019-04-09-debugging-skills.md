---
layout:     post
title:      "Android调试"
subtitle:   " \"调试\""
date:       2019-04-09 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - 调试
    - 模拟
---

# Android调试

## Android 模拟器无法上网
```bash
/Users/eric/Library/Android/sdk/emulator/emulator @Nexus_5X_API_28 -dns-server 8.8.8.8,114.114.114.114
```

## Chrome模拟微信：
当前谷歌版本号： Version 76.0.3809.100 (Official Build) (64-bit)
设置方法： 
Developer Tools -> More Tools -> Network conditions -> User agent

**1.安卓微信UA**
> mozilla/5.0 (linux; u; android 4.1.2; zh-cn; mi-one plus build/jzo54k) applewebkit/534.30 (khtml, like gecko) version/4.0 mobile safari/534.30 micromessenger/5.0.1.352  

**2.Ios微信UA**
> mozilla/5.0 (iphone; cpu iphone os 5_1_1 like mac os x) applewebkit/534.46 (khtml, like gecko) mobile/9b206 micromessenger/5.0 