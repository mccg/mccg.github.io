---
layout: post
title: "解决 error while loading shared libraries"
category: Dev
tags: ["linux", "ldconfig"]
date: 2018-01-01
---

>**引言**:
有的时候动态链接库的位置不在系统受信的目录下，
运行项目时可能会出现找不到 shared libraries 。
在此记录一下 CentOS 下比较优雅的解决步骤。

## Error
- xxxxxx: error while loading shared libraries: libxxxxxx.so.x.x:
  cannot open shared object file: No such file or directory

## Solution
- -1- 找到所需要的动态链接库的文件:
  - `find / -name "libxxxxxx.so.x.x"`
- -2- 将路径添加到 `/etc/ld.so.conf.d/` 目录下:
  - `echo directory-path-of-libraries > /etc/ld.so.conf.d/my-software-name.conf`
- -3- 运行 `ldconfig`
