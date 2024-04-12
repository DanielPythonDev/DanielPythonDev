---
layout: post
title: "Python与环境变量"
date:  2024-04-10 10:14:54
categories: 环境变量
tags: 环境变量
excerpt: Python与环境变量
mathjax: true
---

本文联合创作：@Hanhan666666 & @sky96111

# 环境相关

## python多版本共存

安装多个版本的python，需要安装在不同的目录下，全部添加到环境变量。```where python```和```where pip```操作会告诉你目前环境变量中包含哪些python。使用诸如vscode、pycharm的IDE可以很方便的指定指定版本的python，创建虚拟环境。

当然也有手动方案。在对应目录下python.exe和pip.exe复制一份，然后重命名到python310.exe和pip310.exe，也就是加上版本号。这不一定管用，请确保python310.exe同目录下存在```python310.dll```。


## 环境变量

### cmd操作
在cmd里输入```%path%```得到环境变量。在powershell里面没用，会导致炸环境变量。

临时添加
```
path = %path%;C:\ProgramData\anaconda3\Scripts;C:\ProgramData\anaconda3
```

永久添加到用户
```
SETX path "%path%;C:\ProgramData\anaconda3\Scripts;C:\ProgramData\anaconda3" 
```

永久添加到系统
```
SETX /M path "%path%;C:\ProgramData\anaconda3\Scripts;C:\ProgramData\anaconda3" 
```

### powershell操作

查询环境变量：简单的写法```$env:path```，可以解决问题，但更标准的写法是```Write-Output $env:path```

## 使用scoop包管理器

一键安装scoop脚本
```
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

搜索python包
```
scoop search python
```

安装python：请务必指定版本
```
scoop install python310
scoop reset python312
```
