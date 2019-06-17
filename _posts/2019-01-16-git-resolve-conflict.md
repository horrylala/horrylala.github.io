---
layout:     post
title:      "git实用操作"
subtitle:   " \"疑难问题解决记录\""
date:       2019-01-16 22:05:00
author:     "Horrylala"
header-img: "img/post-bg-git.jpg"
catalog: true
tags:
    - Git
    - Conflict
---

## git pull 冲突解决
当使用*git pull*命令时，如果提示有本地文件修改了，无法合并的时候，我们可以需要先提交，然后在更新。
```bash
git commit
```

如果要放弃本地修改后更新：
```bash
git reset --hard
git pull
```