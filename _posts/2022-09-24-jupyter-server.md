---
layout: post
title:  "How to build online jupyter notebook server 搭建jupyter notebook(anaconda)"
date:  2022-09-24 00:14:54
categories: python jupyter notebook anaconda
tags: python jupyter notebook anaconda
excerpt: 搭建远程的在线jupyter notebook服务，便于远程写代码。
mathjax: true
---

打开```cmd```，输入这个命令，并找到对应的文件
```jupyter notebook --generate-config```

![image](https://user-images.githubusercontent.com/63193298/192081057-e2644c79-2b74-49e7-8ab2-b308d756fc4c.png)

这是一个.py文件，打开对应的目录进行修改即可。

 
设置ip，可以根据安全需要，设置成合适的。 
![image](https://user-images.githubusercontent.com/63193298/192081089-319d8a22-10bd-41b6-92ba-0f19311f0058.png)

修改目录：可以改到D盘，E盘……合适的目录。
![image](https://user-images.githubusercontent.com/63193298/192081092-c56dc00f-4ead-4e17-9dc4-3d5bc3980256.png)

修改密码：这样也可以，但不推荐
![image](https://user-images.githubusercontent.com/63193298/192081106-f8e5d415-81cf-453b-bd8f-d27348197749.png)

最好是通过这个方式设置密码
![image](https://user-images.githubusercontent.com/63193298/192081122-a4a55096-43e9-4eef-9eee-9db1e54be6fb.png)

设置允许远程访问
![image](https://user-images.githubusercontent.com/63193298/192081145-7713251e-7db9-4c20-8821-12e4dbb02334.png)

可以修改一下端口号
![image](https://user-images.githubusercontent.com/63193298/192081149-477c8c46-ec27-4e15-a97c-d28e1a52e7d0.png)

取消token设置，设置为仅通过密码登录
![image](https://user-images.githubusercontent.com/63193298/192081161-84f119fb-efa5-4716-abf7-e29e2cb1df4e.png)
 

本地已经打开了。
![image](https://user-images.githubusercontent.com/63193298/192081129-91a87932-449a-4543-ac68-a60246b6ae74.png)

在这些配置好后，如果本地可以打开，远程其他机器未打开，请在防火墙允许该端口的出入站规则，以及检查路由器是否开启了AP隔离等。
![image](https://user-images.githubusercontent.com/63193298/192081135-173bf9cf-7014-484f-8d4e-49f3e540732e.png)

