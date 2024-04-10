---
layout: post
title:  "Summarize of Linear Algebra 线性代数内容总结（1）"
date:  2022-04-04 06:14:54
categories: Linear Algebra
tags: Linear Algebra
excerpt: 线性代数内容总结
mathjax: true
---


# 矩阵（matrix）

矩阵是一个二维的数表，其中n行1列（n-by-1）称作列向量，我们后面所说的向量都是这个；其中1行n列（1-by-n）的称作行向量。

定义矩阵$ (A)_m\times n $

## 矩阵运算

### 矩阵的加减法
若矩阵$A+B$，则对应矩阵$A,B$必须是同类型矩阵（行数列数相同），对应元素向加减。

### 矩阵的乘法
若矩阵$ A\times B $，若A是mxn矩阵，B为pxq矩阵，必须有n=p。

### 矩阵的逆运算

若一个矩阵存在，$ A\times B=B\times A= I $，则称矩阵$B$ 为矩阵$A$的逆矩阵，记为$A^-1=B$
