---
layout: post
title: "Git：中文乱码"
date: 2020-10-01 14:00:00 +0800
categories: Git
tags: Git 中文乱码
---

> 摘要：在通过 git status 查看项目状态时，文件名出现中文乱码

## 解决方法

输入以下命令：

```shell
git config --global core.quotepath false
```

效果如图：

![截屏2020-10-04 下午2.16.43](/Users/tjc/Pictures/md-picture/截屏2020-10-04 下午2.16.43.png)

红色部分就是文件名，输入之前乱码，输入之后乱码解决。