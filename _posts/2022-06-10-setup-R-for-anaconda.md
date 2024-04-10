---
layout: post
title:  "为anaconda配置4.x版本的R语言"
date:  2022-06-10 00:14:54
categories: R语言 anaconda
tags: R语言 anaconda
excerpt: 默认安装的版本好旧啊QaQ
mathjax: true
---


# anaconda与R语言

anaconda默认提供的R语言版本最高为3.6.1，而目前R语言最新版本为4.2.0，在实际体验过程中，我选择自行安装R语言和RStudio。

![image](https://user-images.githubusercontent.com/63193298/172967429-c8d886ee-9195-4713-a57e-dca3449fa1c1.png)


# 解决方案

本文以下内容参考了stackexchange中此篇回答。源地址https://datascience.stackexchange.com/questions/77335/anconda-r-version-how-to-upgrade-to-4-0-and-later

执行以下代码

```
conda create --name r4-base
conda activate r4-base
conda install -c conda-forge r-base=4.1.3
conda install -c conda-forge/label/gcc7 r-base=4.1.3
```

目前只有4.1.3版本，最新的4.2.0还不可以。过段时间或许就可以支持了，后续的读者可以尝试改成4.2.0

![image](https://user-images.githubusercontent.com/63193298/172969960-70c570ba-ff3e-4dd5-8223-d8a6d33243be.png)

可以安装R语言，但至于新版的rstudio还是放弃吧。这个版本两年没有更新了。原帖地址
https://community.rstudio.com/t/how-do-i-update-the-version-of-rstudio-in-anaconda/39799/2



