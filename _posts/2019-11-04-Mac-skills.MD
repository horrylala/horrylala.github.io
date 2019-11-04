---
layout:     post
title:      "Mac 安装技巧合集"
subtitle:   " \"Mac软件\""
date:       2019-11-04 8:15:00
author:     "Horrylala"
header-img: "img/micro-front.jpeg"
catalog: true
tags:
    - 滚动
    - 视口
---

# Mac 安装技巧合集
## 安装Go2Shell

```bash
open -a Go2Shell --args config
```
打开finder窗口，按住command键，拖动。

## iterm乱码

在iterm中设置：
> preference -> profiles -> Default -> Text -> use a different for a non-ASCII text -> 

## vscode

vscode并打开命令面板```⇧⌘P```，然后输入 *shell command* 找到: *Install ‘code' command in PATH*。

打开文件夹：
```
code folder
```

## 安装[oh-my-zsh](https://ohmyz.sh/)
```
vim ~/.zshrc
ZSH_THEME=""
```
## 安装[Powerline fonts](https://github.com/powerline/fonts)
* clone
```
git clone https://github.com/powerline/fonts.git --depth=1
```
* install
```
cd fonts
./install.sh
```
* clean-up a bit
```
cd ..
rm -rf fonts
```

# lrzsz
```
yum -y install lrzsz
```

## Chrome跨域
### Mac设置跨域：

* chrome49以前版本
```bash
open -a "Google Chrome" --args --disable-web-security
```
* chrome49以后版本
```bash
open -n /Applications/Google\ Chrome.app --args --disable-web-security --user-data-dir=/Users/599290/data/chrome-user-data  
```

## Safari设置跨域
```bash
open -a '/Applications/Safari.app' --args --disable-web-security
```
## Window：
```bash
chrome.exe --disable-web-security --user-data-dir=/Users/599290/data/chrome-user-data  
```

> Mac-->Chrome如果命令行不成功可以安装一个插件Allow-Control-Allow-Origin

## registry
常用镜像：[淘宝镜像](https://registry.npm.taobao.org), 

使用方法：
> npm install loadsh --registry=https://registry.npm.taobao.org


## node版本
node版本切换，使用*n*。
```bash
node -v
sudo n 9.9.0
```

## 解压
```bash
unzip archive.zip -d "/home/data/"
```