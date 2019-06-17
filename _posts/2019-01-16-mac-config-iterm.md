---
layout:     post
title:      "Mac下使用iTerm和oh-my-zsh"
subtitle:   " \"超级好用的mac命令行工具\""
date:       2019-01-16 22:05:00
author:     "Horrylala"
header-img: "img/post-bg-wallhaven.jpg"
catalog: true
tags:
    - Mac
    - tools
---


# iTerm2
App Store下载[iTerm2](https://iterm2.com/downloads.html)，进行安装。

# Go2Shell
*[Go2Shell]((https://itunes.apple.com/cn/app/go2shell/id445770608))*是Mac上的一个小萌物，可以快速打开terminal。
把它拖到*Finder*工具栏上，点击后可直接在当前目录下开启终端。省了再*cd*的麻烦。

它默认是打开系统的*term*，如果希望设置：
```bash
open -a Go2Shell --args config
```
打开后选择*iTerm2*
![Go2Shell-config.png](/img/in-post/post-mac-tool/Go2Shell-config.png)

设置完毕之后，将小图标拖动到finder窗口。
*ALT + SPACE*打开spot，输入*go2shell*,按住command键，拖动app到finder标题栏。

![go2shell-drag.png](/img/in-post/post-mac-tool/go2shell-drag.png)

# Alfred
Alfred为Mac上又一大利器。


# 在iTerm上打开vscode

> * 1.VS code并打开命令面板（ ⇧⌘P ）
> * 2.输入 shell command 找到: Install ‘code' command in PATH 。

vscode打开folder:
```bash
code folder
```

# oh-my-zsh
[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh/)提供了便捷的iTerm样式美化。
## 安装
```bash
# curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# wget
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
执行完，发现不生效，调用*source ~/.zshrc*发现报错：
```bash
bash: autoload: command not found
bash: /Users/ericwang/.oh-my-zsh/oh-my-zsh.sh: line 34: syntax error near unexpected token `('
bash: /Users/ericwang/.oh-my-zsh/oh-my-zsh.sh: line 34: `for config_file ($ZSH/lib/*.zsh); do'
```
查询资料，得知是zsh不是默认的terminal。
执行下面这句就OK。
```bash
chsh -s $(which zsh)
```
## 配置theme和plugin
```bash
> vi ~/.zshrc
# 修改参数：
ZSH_THEME="" # "random"或者固定的theme

plugins=(
  git
  bundler
  dotenv
  osx
  rake
  rbenv
  ruby
)

```

## Powerline fonts
[Powerline fonts](https://github.com/powerline/fonts)是一些theme的字体信息，一些特殊的theme需要这些字体。
```bash
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

在iterm中设置：
preference -> profiles -> Default -> Text -> use a different for a non-ASCII text -> [选择一款以Powerline 结尾的字体]


