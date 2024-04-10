---
layout: post
title:  "How to build online jupyter lab server 搭建jupyter lab(anaconda)"
date:  2022-11-21 00:14:54
categories: python jupyter lab anaconda
tags: python jupyter lab anaconda
excerpt: 搭建远程的在线jupyter lab服务，便于远程写代码。之前不是弄了一个notebook嘛，发现了一个更好用的jupyter lab
mathjax: true
---


与jupyter notebook的操作相仿，而jupyter LAB更是支持了深色模式。建议配置好8888、8889、8890往下的几个端口，以便应对可能出现的bug。此外，也用来当作临时的HTTP Server以存储文件。搭配ddns-go使用，在一定程度下可以避免域名变更带来的不便。

打开```cmd```，输入这个命令，并找到对应的文件
```jupyter lab --generate-config```

![image](https://user-images.githubusercontent.com/63193298/203014392-851ff3cd-4a2a-4f0a-a8f4-eccba2e94297.png)


这是一个.py文件，打开对应的目录进行修改即可。（这次还是不要用记事本了嘿嘿）


设置ip，可以根据安全需要，设置成合适的。 

```
## The IP address the Jupyter server will listen on.
#  Default: 'localhost'
# c.ServerApp.ip = 'localhost'
```

修改为如下（为空代表所有IP）

```
## The IP address the Jupyter server will listen on.
#  Default: 'localhost'
c.ServerApp.ip = ''
```

修改目录：可以改到D盘，E盘……合适的目录。
```
## DEPRECATED, use root_dir.
#  Default: ''
# c.ServerApp.notebook_dir = ''
```
```
## Preferred starting directory to use for notebooks and kernels.
#  Default: ''
# c.ServerApp.preferred_dir = ''
```
修改为如下（可以设置C盘、D盘等等的任意路径）
```
## DEPRECATED, use root_dir.
#  Default: ''
c.ServerApp.notebook_dir = r'D:\jupyter'
```
```
## Preferred starting directory to use for notebooks and kernels.
#  Default: ''
c.ServerApp.preferred_dir = r'D:\jupyterLab'
```

修改密码：最好是通过这个方式设置密码
![image](https://user-images.githubusercontent.com/63193298/203016862-9e8fe0ac-aa2e-4987-a0ae-a3febff81c30.png)
温馨提示：输入时没有提示是正常的

设置允许远程访问
```
## Hostnames to allow as local when allow_remote_access is False.
#  
#         Local IP addresses (such as 127.0.0.1 and ::1) are automatically accepted
#         as local as well.
#  Default: ['localhost']
# c.ServerApp.local_hostnames = ['localhost']
```

```
## Hostnames to allow as local when allow_remote_access is False.
#  
#         Local IP addresses (such as 127.0.0.1 and ::1) are automatically accepted
#         as local as well.
#  Default: ['localhost']
c.ServerApp.local_hostnames = ['localhost']
```


取消token设置，设置为仅通过密码登录
```
## Token used for authenticating first-time connections to the server.
#  
#          The token can be read from the file referenced by JUPYTER_TOKEN_FILE or set directly
#          with the JUPYTER_TOKEN environment variable.
#  
#          When no password is enabled,
#          the default is to generate a new, random token.
#  
#          Setting to an empty string disables authentication altogether, which
#  is NOT RECOMMENDED.
#  Default: '<generated>'
# c.ServerApp.token = '<generated>'
```

```
## Token used for authenticating first-time connections to the server.
#  
#          The token can be read from the file referenced by JUPYTER_TOKEN_FILE or set directly
#          with the JUPYTER_TOKEN environment variable.
#  
#          When no password is enabled,
#          the default is to generate a new, random token.
#  
#          Setting to an empty string disables authentication altogether, which
#  is NOT RECOMMENDED.
#  Default: '<generated>'
c.ServerApp.token = ''
```

本地已经打开了。
![image](https://user-images.githubusercontent.com/63193298/192081129-91a87932-449a-4543-ac68-a60246b6ae74.png)

在这些配置好后，如果本地可以打开，远程其他机器未打开，请在防火墙允许该端口的出入站规则，以及检查路由器是否开启了AP隔离等。
![image](https://user-images.githubusercontent.com/63193298/192081135-173bf9cf-7014-484f-8d4e-49f3e540732e.png)

