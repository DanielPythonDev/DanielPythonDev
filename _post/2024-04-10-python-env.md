---
layout: post
title:  "Python与环境变量"
date:  2024-04-10 06:14:54
categories: 环境变量
tags: 环境变量
excerpt: Python与环境变量
mathjax: true
---


# 环境相关
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
