---
layout:     post
title:      "Linux常用命令"
subtitle:   " \"linux常用命令\""
date:       2018-12-10 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - linux
---

# Linux常用命令

## 查看os等信息：
```bash
cat /proc/version
```

## 查看cpu信息，包括型号、主频、内核信息等
```bash
cat /proc/cpuinfo
# 或者
lscpu
```

## 查看硬盘信息：
```bash
fdisk -l
```

## 解压缩
tar -zxvf

## openresty
Openresty，Scalable Web Platform by Extending NGINX with Lua。
```bash
# add repo（centos）
sudo yum install yum-utils
sudo yum-config-manager --add-repo https://openresty.org/package/centos/openresty.repo
# Then you can install a package, say, openresty, like this:
sudo yum install openresty

# or (download binary files)
tar -xvf openresty-VERSION.tar.gz
cd openresty-VERSION/
./configure -j2
make -j2
sudo make install

# better also add the following line to your ~/.bashrc or ~/.bash_profile file.
export PATH=/usr/local/openresty/bin:$PATH
```
如果提示*install the PCRE library*类似消息时：
```bash
yum install pcre-devel openssl-devel gcc curl
```

## 用户操作
### root 登录
```bash
[liuhai@localhost ~]$ su root
Password: 
```

### 用户赋权
改变目录的所有者 赋予opt目录给liuhai这个用户赋权：
```bash
chown -R liuhai:liuhai /opt
```
```bash
chmod 760 /opt
```
赋予opt目录读写权限给liuhai，别的用户对这个目录没有任何权限。

### 创建用户
```bash
useradd appdeploy
userpw appdeploy
```

然后输入appdeploy的密码。

### 切换用户
```bash
su appdeploy
```

### 给appdeploy赋权
```bash
chown - R wang.users data/
```

### kill 进程大法
```bash
ps -ef | grep start | grep -v grep | cut -c 11-17 | xargs kill -9
```

## vim 常用操作命令
返回 u
到顶部 gg
到底部 G
到5行  5 + G
到行首 shift + 6 / h
到行尾 shift + 4 
到下一个单词 E 
到一页最前面 shift + h

列编辑 ctrl + v
1)d删除选中
2)shift + I(i) 输入完成之后，两次ESC

y + y 复制当前行， p粘贴到下一行