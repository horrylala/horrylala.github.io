---
layout:     post
title:      "centos安装git"
subtitle:   " \"git\""
date:       2019-06-17 11:14:00
author:     "Horrylala"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - git
---

# Using Dit At CentOs

## Install git
```bash
yum -y install git
```

## Generate SSH key
```bash
ssh-keygen -t rsa -C "horrylala@outlook.com"
```
连续几个回车空格，得到id_rsa和id_rsa.pib，在/root/.ssh下面，说明生产成功。

## Github中添加密钥
* 1.在[Github](http://www.github.com/)中，登录自己的账号。
* 2.点击自己的头像->settings->SSH And GPG Keys->New SSH key。
* 3.将本地 id_rsa.pub 中的内容粘贴到 Key 文本框中，随意输入一个 title(不要有中文)，点击 Add Key 即可。

## 验证
命令行输入：
```bash
ssh git@github.com
```

出现如下询问：
```bash
Are you sure you want to continue connecting (yes/no)?
```

键入yes后回车，如果出现：
```bash
Hi ***! You've successfully authenticated, but GitHub does not provide shell access.
```
则表明验证成功。

## 使用
git常用命令
> git clone url
> git checkout master
> git pull
> git push

