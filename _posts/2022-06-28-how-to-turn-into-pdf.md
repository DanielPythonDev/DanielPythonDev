---
layout: post
title:  "【办公小技巧】 How to create PDF file and transfer with WORD  如何创建PDF  WORD与PDF互转"
date:  2022-06-28 00:14:54
categories: Python 办公 PDF 小技巧
tags: Python 办公 PDF 小技巧
excerpt: 办公软件教学：上交材料需要PDF文件？Word文档到其他电脑容易错乱，另存为PDF，打印很方便喵~
mathjax: true
---

以往笔者在生成PDF文档的过程中，生成的PDF文档往往较大，或者一定程度上依赖第三方软件。这些软件虽然有绿色软件，但也不乏一些需要安装，甚至可能存在一定的安全漏洞的软件。此外，一些体积较大或涵盖重要内容的文档也不宜使用在线服务网站进行操作。因而，掌握一些PDF相关的操作方法与技巧是有必要的。

# 由文稿生成PDF文档

对于已经完成的office软件文稿，另存为PDF可以采取如下两种方法。

## 方法1：对文件进行另存为，选择PDF

![image](https://user-images.githubusercontent.com/63193298/176084860-01d6286d-8d75-4245-914a-66b33c9054a6.png)

如果压缩过后PDF大小仍较大，可以通过优化图片缩小最终生成的PDF文档大小。

![image](https://user-images.githubusercontent.com/63193298/176085913-a2b5f3b2-6611-40ba-ac7e-8fd261177495.png)

勾选“最小文件大小”和“优化图像质量”是推荐的。

## 方法2：对文件进行打印，选择打印机“Microsoft to PDF”

![image](https://user-images.githubusercontent.com/63193298/176084967-740f6c72-936c-465e-b97e-028a2854c1ba.png)

打印后，选择保存的文档。此方法类似于预打印，可以预览打印后的效果。


# 由图片生成PDF文档

## 方法1：生成Word文档进行打印。

这种操作不推荐，因为往往生成的文档会比较大，除非有一定的额外的文字编辑需求。

## 方法2：右键打印。

选中图片，右键打印。

![image](https://user-images.githubusercontent.com/63193298/176086489-7208ead5-6835-4a9e-8a79-2513bc6f95c7.png)

缺点是会忽略图片本身的横竖排列，如果具有多个横竖不一致的图片，需要分开打印。（右下角 【选项】->【打印机属性】可以设置横向和纵向）

## 方法3：使用Python代码生成PDF

这个方法需要一定的编程能力。建议有一定基础的读者使用。

需要安装的python模块是`fitz`。

```
import fitz
import os
img_path = 'G:\\vo\\bk'
doc = fitz.open()

# 循环path中的文件，可import os 然后用 for img in os.listdir(img_path)实现
# 这里为了让文件以1，2，3的形式进行拼接，就偷懒循环文件名中的数字。
for img in os.listdir(img_path):

	img_file = img_path + '\\' + img
	imgdoc = fitz.open(img_file)
	pdfbytes = imgdoc.convertToPDF()
	pdf_name = img + '.pdf'
	imgpdf = fitz.open(pdf_name, pdfbytes)
	doc.insertPDF(imgpdf)
doc.save('combined.pdf')
doc.close()

```

# PDF合并 - 使用Python代码实现

过去笔者曾经使用过福昕阅读器的装订器功能，但整个软件过于庞大，因而使用python取代这个软件。

需要安装Python库`PyPDF2`。`pdf_files`中的元素请自行添加。

```
from PyPDF2 import PdfFileReader, PdfFileMerger

pdf_files=[]

result_pdf=PdfFileMerger()

for pdf in pdf_files:
	with open(pdf, 'rb') as fp:
		pdf_reader =PdfFileReader(fp)
		if pdf_reader.isEncrypted:
			print('ignore encrypted file')
			continue
		result_pdf.append(pdf_reader, import_bookmarks=True)

result_pdf.write('result.pdf')
result_pdf.close()

```

