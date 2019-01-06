---
layout:     post
title:      "Jekyll Install"
subtitle:   " \"Hello World, 第一篇博客\""
date:       2018-12-20 21:00:00
author:     "Horrylala"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Jekyll
    - Blog
---

> “Yeah It's on. ”

## jekyll安装

```bash
xcode-select --install #  install the command-line tools
gem install --user-install bundler jekyll # home directory

# .~/.bash_profile or ~/.bashrc
export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
```
## 出现问题
```bash
active developer path ("/Applications/Xcode.app/Contents/Developer") does not exist
Use `sudo xcode-select --switch path/to/Xcode.app` to specify the Xcode that you wish to use for command line developer tools, or use `xcode-select --install` to install the standalone command line developer tools.
```

问题分析：
定位到xcode安装失败，或者未安装。
本例中没有安装xcode。

解决方案：
```bash
xcode-select --install # 单独安装CommandLineTools，不需要Xcode
sudo xcode-select --switch /Library/Developer/CommandLineTools  # 指定路径
```

解决这一步之后，提示安装成功。但是有一个warning:
```bash
You don't have /Users/ericwang/.gem/ruby/2.3.0/bin in your PATH,
	  gem executables will not run.
```
选择了忽略。
但是在执行`jekyll`时，提示`jekyll: command not found`

```bash
# 将这一行加入到.bash_profile中
/Users/ericwang/.gem/ruby/2.3.0/bin
source .bash_profile
```
然后就OK了

```bash
jekyll new myblog
cd myblog
bundle exec jekyll serve
```