---
title: 数据库远程复制，导入到本地
date: 2014-11-24 10:33:07
tags: mysql
---

eg. 从主机1.1.1.1复制数据库到本地

+  mysqldump   -h1.1.1.1   -u用户名    -p密码  数据库名 >  temp.sql

+  登录本地MySQL

+  选择要导入的数据库， use temp

+  source temp.sql 