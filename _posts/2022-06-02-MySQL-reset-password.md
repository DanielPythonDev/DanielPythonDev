---
layout: post
title:  "MySQL 8.0 忘记密码 或 重置密码"
date:  2022-06-02 00:14:54
categories: MySQL8.0 忘记密码 重置密码
tags: MySQL8.0 忘记密码 重置密码
excerpt: 折腾了好久，原来如此
mathjax: true
---

笔者多年前曾遇到过这个问题，并在CSDN上写过文章。考虑到这个问题，笔者曾经为止困扰许久，且网络上的资料大多过时（仍然是针对MySQL5.7版本），遂今天数据库原理课下课后，做了重新整理，并发表在自己的博客上。

# MySQL初始化
## Linux-以Ubuntu为例

我在ubuntu20.04系统下使用apt安装的mysql8.0，安装时未提示设置root用户密码。（如果遇到提示，那么就按照提示设置初始密码即可）

使用命令`sudo cat /etc/mysql/debian.cnf` 查看mysql的默认密码
![image](https://user-images.githubusercontent.com/63193298/171538270-1932aa6b-b9f0-4be4-90bd-a664b384f160.png)

password后面的可以复制下来，这就是root账号的密码。

登陆成功。接下来修改密码。MySQL8.0有个新功能将原有5.7中的某个命令取消了而增强了安全性。

接下来使用命令`alter user 'root'@'localhost' identified with mysql_native_password by '123456'`

将root用户的密码修改成123456。这里还可以修改成其他密码。

已经修改完成。接下来可以用新密码登陆了。

## Windows如何初始化

一般而言，安装过程中会提示设置密码。但在实际过程中，也有安装过程中未设置密码的情况。对此，可以用管理员身份打开cmd，在相关目录下，输入以下命令

设置为空密码： `mysqld --initialize-insecure`

自主设置密码： `mysqld --initialize`

# 重置密码

windows与linux系统上的MySQL重置密码方式都比较相似。MySQL8.0引入了新的安全机制，废除了password()函数。使用命令`alter user 'root'@'localhost' identified with mysql_native_password by '123456'`

将root用户的密码修改成123456。这里还可以修改成其他密码。

# 忘记密码

通过命令 `mysqld --skip-grant-tables` 跳过，并重新登录。
