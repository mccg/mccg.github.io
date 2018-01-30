---
layout: post
title: "忘记 XX 密码 系列"
category: Dev
tags: ["password", "shell"]
date: 2017-06-07

---

>**引言**:
在这里记录一下丢失 XX 密码的解决方案中的重要信息。

## 忘记 CentOS7 root 密码
- 启动后按`e`, 在LANG 行后面加 `init=/bin/sh`
- 进入 `sh` 后 使用 `passwd` 来设置密码。

## 忘记 mysql root 密码
- `service mysqld stop`
- `mysqld_safe --skip-grant-tables &`
- `/etc/my.cnf` => `[mysqld] skip-grant-tables=1`
- `mysql -uroot`
- `mysql 5.7`: `update mysql.user set authentication_string = password('123'), password_expired = 'N', password_last_changed = now() where user = 'root';`


