Python开发常用语句命令脚本笔记 

Daniel, 2024-04-01

# 环境相关
## 环境变量

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

## 镜像源

### pip换源操作

比如更换到清华源，可以使用下面的命令：

```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

中科大pypi源已经撤了，目前被重定向至北京外国语大学，所以仍可用。这个源速度还比较快，值得推荐。

```
pip config set global.index-url https://mirrors.bfsu.edu.cn/pypi/web/simple
```

### 多源操作
pip支持多镜像源，即一个镜像源不可使用时自动切换到下一个。于是，在不同的网络环境下，显得比较方便。
```
pip config set global.extra-index-url "<url1> <url2>..."
```
我目前使用的就是这一组镜像源方案，虽然比较累赘，不过实际体验来说对不同的网络环境比较强的鲁棒性。建议读者根据自己的网络环境做一些调整。具体可参考[校园网联合镜像源](https://mirrors.cernet.edu.cn/list/pypi)，
```
pip config set global.extra-index-url "https://mirrors.bfsu.edu.cn/pypi/web/simple https://pypi.tuna.tsinghua.edu.cn/simple https://pypi.mirrors.ustc.edu.cn/simple https://mirrors.aliyun.com/pypi/simple/"
```
# 基础知识
## 变量范围

在Python中，当你在函数内部读取一个在外部定义的变量时，Python 允许你读取这个变量的值而不需要任何特殊声明。但是，如果你尝试在函数内部修改一个外部定义的变量（即赋予它一个新的值），Python 会将这个变量视为函数内部的一个新局部变量，除非你明确地告诉 Python 这个变量是全局变量。

## 程序结构
python 3.8新引入switch结构

```
match var:
    case a:
        function
    case b:
        function
    case _:
        default
```


# 基本数据结构和对象

## 对象类别匹配
匹配：如果```key```和后面的```tuple```是同类
```
isinstance(key, tuple)
```
## 字符串处理

```"".strip()```方法去除一些换行符、空格之类的字符

```"".rstip()```字符串操作 Remove spaces at the beginning and at the end of the string:

## dict 字典 

### 默认值


```
# 全局性默认值 在定义的时候就加上去
from collections import defaultdict


# 局部个案性默认值
car = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

x = car.setdefault("model", "Bronco")
y = car.setdefault("model1", "Tesla")
```
https://www.w3schools.com/python/ref_dictionary_setdefault.asp

### 合并两个字典

Python3的老方法(1): ```dict1```和```dict2```直接合并到```dict2```上。
```
dict2.update(dict1)
```

Python3的老方法(2): ```dict1```和```dict2```直接合并到新的```res```上。冲突时最后一个有效。
```
res = {**dict1, **dict2}
```

Python3.9引入的新方法：如有冲突最后一个有效。
```
res1 = dict1 | dict2
res2 = dict2 | dict1
```
加强版
```
dict2 |= dict1
```


# 文本处理


## Unicode常见中文乱码速查表

xxxxxx   | 示例 | 特点 | 产生原因
------|------|-----|---------|
古文码 | 鐢辨湀瑕佸ソ濂藉涔犲ぉ澶╁悜涓? | 大都为不认识的古文，并加杂日韩文 | 以 GBK 方式读取 UTF-8 编码的中文 |
口字码 | ����Ҫ�¨2�ѧϰ������ | 大部分字符为小方块 | 以 UTF-8 的方式读取 GBK 编码的中文 |
符号码 | ç”±æœˆè\|å￥½å￥½å-\|ä1 å¤©å¤©å‘ä¸Š | 大部分字符为各种符号 | 以 ISO8859-1 方式读取 UTF-8 编码的中文 |
拼音码 | óéÔÂòaoÃoÃÑ§Ï°ììììÏòéÏ | 大部分字符为头顶带有各种类似声调符号的字母 | 以 ISO8859-1 方式读取 GBK 编码的中文 |
问句码 | 由月要好好学习天天向?? | 字符串长度为偶数时正确，长度为奇数时最后的字符变为问号 | 以 GBK 方式读取 UTF-8 编码的中文，然后又用 UTF-8 的格式再次读取 |
锟拷码 | 锟斤拷锟斤拷要锟矫猴拷学习锟斤拷锟斤拷锟斤拷 | 全中文字符，且大部分字符为“锟斤拷”这几个字符 | 以 UTF-8 方式读取 GBK 编码的中文，然后又用 GBK 的格式再次读取 |
烫烫烫 | 烫烫烫烫烫烫烫烫烫烫烫烫烫烫烫烫烫烫 | 字符显示为“烫烫烫”这几个字符 | VC Debug 模式下，栈内存未初始化 |
屯屯屯 | 屯屯屯屯屯屯屯屯屯屯屯屯屯屯屯屯屯屯 | 字符显示为“屯屯屯”这几个字符 | VC Debug 模式下，堆内存未初始化 |

## 内置字符串
```
import string
string.ascii_uppercase
string.ascii_lowercase
string.ascii_letters
```
## 正则表达式

### 简单例子

```
import re
re.findall(re_exp, finddata, '')
```

### 常用正则表达式
#### 一、校验数字的表达式

数字：```^[0-9]*$```

n位的数字：```^\d{n}$```

至少n位的数字：```^\d{n,}$```

m-n位的数字：```^\d{m,n}$```

零和非零开头的数字：```^(0|[1-9][0-9]*)$```

非零开头的最多带两位小数的数字：```^([1-9][0-9]*)+(\.[0-9]{1,2})?$```

带1-2位小数的正数或负数：```^(\-)?\d+(\.\d{1,2})$```

正数、负数、和小数：```^(\-|\+)?\d+(\.\d+)?$```

有两位小数的正实数：```^[0-9]+(\.[0-9]{2})?$```

有1~3位小数的正实数：```^[0-9]+(\.[0-9]{1,3})?$```

非零的正整数：```^[1-9]\d*$ 或 ^([1-9][0-9]*){1,3}$ 或 ^\+?[1-9][0-9]*$```

非零的负整数：```^\-[1-9][]0-9"*$ ```或``` ^-[1-9]\d*$```

非负整数：```^\d+$``` 或 ```^[1-9]\d*|0$```

非正整数：```^-[1-9]\d*|0$``` 或 ```^((-\d+)|(0+))$```

非负浮点数：```^\d+(\.\d+)?$``` 或 ```^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$```

非正浮点数：```^((-\d+(\.\d+)?)|(0+(\.0+)?))$``` 或 ```^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$```

正浮点数：```^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$``` 或 ```^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$```

负浮点数：```^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$``` 或 ```^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$```

浮点数：```^(-?\d+)(\.\d+)?$``` 或 ```^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$```
#### 二、校验字符的表达式

汉字：```^[\u4e00-\u9fa5]{0,}$```

英文和数字：```^[A-Za-z0-9]+$``` 或 ```^[A-Za-z0-9]{4,40}$```

长度为3-20的所有字符：```^.{3,20}$```

由26个英文字母组成的字符串：```^[A-Za-z]+$```

由26个大写英文字母组成的字符串：```^[A-Z]+$```

由26个小写英文字母组成的字符串：```^[a-z]+$```

由数字和26个英文字母组成的字符串：```^[A-Za-z0-9]+$```

由数字、26个英文字母或者下划线组成的字符串：```^\w+$``` 或 ```^\w{3,20}$```

中文、英文、数字包括下划线：```^[\u4E00-\u9FA5A-Za-z0-9_]+$```

中文、英文、数字但不包括下划线等符号：```^[\u4E00-\u9FA5A-Za-z0-9]+$ 或 ^[\u4E00-\u9FA5A-Za-z0-9]{2,20}$```

可以输入含有```^%&',;=?$\"```等字符：```[^%&',;=?$\x22]+```

禁止输入含有~的字符：```[^~]+```
#### 三、特殊需求表达式

Email地址：```^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$```

域名：```[a-zA-Z0-9][-a-zA-Z0-9]{0,62}(\.[a-zA-Z0-9][-a-zA-Z0-9]{0,62})+\.?```

InternetURL：```[a-zA-z]+://[^\s]* 或 ^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$```

手机号码：```^(13[0-9]|14[01456879]|15[0-35-9]|16[2567]|17[0-8]|18[0-9]|19[0-35-9])\d{8}$```

电话号码("XXX-XXXXXXX"、"XXXX-XXXXXXXX"、"XXX-XXXXXXX"、"XXX-XXXXXXXX"、"XXXXXXX"和"XXXXXXXX)：```^(\(\d{3,4}-)|\d{3.4}-)?\d{7,8}$```

国内电话号码(0511-4405222、021-87888822)：```\d{3}-\d{8}|\d{4}-\d{7}```

电话号码正则表达式（支持手机号码，3-4位区号，7-8位直播号码，1－4位分机号）: ```((\d{11})|^((\d{7,8})|(\d{4}|\d{3})-(\d{7,8})|(\d{4}|\d{3})-(\d{7,8})-(\d{4}|\d{3}|\d{2}|\d{1})|(\d{7,8})-(\d{4}|\d{3}|\d{2}|\d{1}))$)```

身份证号(15位、18位数字)，最后一位是校验位，可能为数字或字符X：```(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)```

帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：```^[a-zA-Z][a-zA-Z0-9_]{4,15}$```

密码(以字母开头，长度在6~18之间，只能包含字母、数字和下划线)：```^[a-zA-Z]\w{5,17}$```

强密码(必须包含大小写字母和数字的组合，不能使用特殊字符，长度在 8-10 之间)：```^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[a-zA-Z0-9]{8,10}$```

强密码(必须包含大小写字母和数字的组合，可以使用特殊字符，长度在8-10之间)：```^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,10}$```

日期格式：```^\d{4}-\d{1,2}-\d{1,2}```

一年的12个月(01～09和1～12)：```^(0?[1-9]|1[0-2])$```

一个月的31天(01～09和1～31)：```^((0?[1-9])|((1|2)[0-9])|30|31)$```

xml文件：```^([a-zA-Z]+-?)+[a-zA-Z0-9]+\\.[x|X][m|M][l|L]$```

中文字符的正则表达式：```[\u4e00-\u9fa5]```

双字节字符：```[^\x00-\xff]``` (包括汉字在内，可以用来计算字符串的长度(一个双字节字符长度计2，ASCII字符计1))

空白行的正则表达式：```\n\s*\r``` (可以用来删除空白行)

HTML标记的正则表达式：```<(\S*?)[^>]*>.*?|<.*? />``` ( 首尾空白字符的正则表达式：```^\s*|\s*$或(^\s*)|(\s*$)``` (可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式)

腾讯QQ号：```[1-9][0-9]{4,}``` (腾讯QQ号从10000开始)

中国邮政编码：```[1-9]\d{5}(?!\d)``` (中国邮政编码为6位数字)

IPv4地址：```((2(5[0-5]|[0-4]\d))|[0-1]?\d{1,2})(\.((2(5[0-5]|[0-4]\d))|[0-1]?\d{1,2})){3}```

#### 四、钱的输入格式：

有四种钱的表示形式我们可以接受:"10000.00" 和 "10,000.00", 和没有 "分" 的 "10000" 和 "10,000"：```^[1-9][0-9]*$```

这表示任意一个不以0开头的数字,但是,这也意味着一个字符"0"不通过,所以我们采用下面的形式：```^(0|[1-9][0-9]*)$```

一个0或者一个不以0开头的数字.我们还可以允许开头有一个负号：```^(0|-?[1-9][0-9]*)$```

这表示一个0或者一个可能为负的开头不为0的数字.让用户以0开头好了.把负号的也去掉,因为钱总不能是负的吧。下面我们要加的是说明可能的小数部分：```^[0-9]+(.[0-9]+)?$```

必须说明的是,小数点后面至少应该有1位数,所以"10."是不通过的,但是 "10" 和 "10.2" 是通过的：```^[0-9]+(.[0-9]{2})?$```

这样我们规定小数点后面必须有两位,如果你认为太苛刻了,可以这样：```^[0-9]+(.[0-9]{1,2})?$```

这样就允许用户只写一位小数.下面我们该考虑数字中的逗号了,我们可以这样：```^[0-9]{1,3}(,[0-9]{3})*(.[0-9]{1,2})?$```

1到3个数字,后面跟着任意个 逗号+3个数字,逗号成为可选,而不是必须：```^([0-9]+|[0-9]{1,3}(,[0-9]{3})*)(.[0-9]{1,2})?$```

备注：这就是最终结果了,别忘了"+"可以用"*"替代如果你觉得空字符串也可以接受的话(奇怪,为什么?)最后,别忘了在用函数时去掉去掉那个反斜杠,一般的错误都在这里



# 时间处理
## 日期

```
from datetime import datetime
current_date = datetime.now()
current_date.strftime('%Y-%m-%d')
```

## 计时

```
import time
start = time.time()
print('程序耗时%s' % round((time.time()-start), 2))
```


# 系统
## 防火墙一键开启端口脚本（管理员）
TCP协议，允许12345端口入站出站
```
netsh advfirewall firewall add rule name="allow_tcp_12345" dir=in action=allow protocol=TCP localport=12345
netsh advfirewall firewall add rule name="allow_tcp_12345" dir=out action=allow protocol=TCP localport=12345
```

UDP协议，允许12345端口入站出站
```
netsh advfirewall firewall add rule name="allow_udp_12345" dir=in action=allow protocol=UDP localport=12345
netsh advfirewall firewall add rule name="allow_udp_12345" dir=out action=allow protocol=UDP localport=12345
```
允许ICMP
```
netsh advfirewall firewall add rule name="ICMP Allow incoming V4 echo request" protocol=icmpv4:8,any dir=in action=allow
```

# 文件读写
## 路径遍历

```
import os
for (root, dirs, files) in os.walk(day_kline_path):
    for file in files:
        file_full_path = os.path.join(root, file)
```

不区分路径和文件，用下面的写法
```
import os
os.listdir()
```

判断路径或文件
```
import os
os.path.isdir()
os.path.isfile()
```


## 判断文件后缀

```
file_name[-4:] == 'gzip'
file_name.split('.')[1] == 'gzip'
file_name.endswith('gzip')
```


## 复制文件
复制文件。这里给了一个随机抽样复制文件的例子
```
import random
import shutil
import os

copy_source = r'D:\zhrwork\20240329\Astock\A股'
copy_destination = r'D:\zhrwork\20240329\Astock\A2股'

POPULATION = []
SAMPLE = []


for (root, dirs, files) in os.walk(copy_source):
    POPULATION = files

SAMPLE = random.sample(POPULATION, 200)
for i in SAMPLE:
    shutil.copy(
        os.path.join(copy_source, i),
        os.path.join(copy_destination, i)
    )
```
## 基本文件读写
这里好像是个语法糖
```
with open(...) as f
    lines = []
        for line in f:
```
## 读写csv文件

```
with open(filepath, encoding='gbk') as f:
    title = f.readline().split(',')
```
使用```csv```库进行优化
```
import csv
with open(filepath, encoding='gbk') as f:
    csvf = csv.writer(f)
    csvf.writerow(title)
    csvf.writerows(resTable1)
```
使用```pandas```库的```read_csv```方法，返回一个```DataFrame```对象
```
import pandas as pd
f = pd.read_csv()
```



## 压缩包读写




### gz/gzip压缩包

## parquet对象

大数据列存标准格式 - Parquet

https://zhuanlan.zhihu.com/p/341572070


需要安装一些库，执行```pip install pyarrow```或```pip install fastparquet```

# pandas专题

使用Pandas读取CSV文件：可以直接使用pandas.read_csv来读取CSV文件，这样可以避免手动解析每一行。Pandas提供了非常高效的数据读取和处理能力。

向量化操作以提高效率：尽量避免使用for循环遍历数据帧中的每一行。Pandas和NumPy都支持向量化操作，可以同时对数据帧或数组中的多个元素进行操作，这通常比循环遍历更快。

减少文件的重复打开：如果在循环中频繁打开和关闭同一个文件，可以考虑一次性读取文件内容到内存中，然后进行操作，这样可以减少I/O开销。

优化数据结构：使用更适合的数据结构，比如Pandas的DataFrame，这样可以利用Pandas库提供的丰富功能，简化很多数据处理任务。


## DataFrame
两种遍历方式
```
for date, row in df.T.iteritems():
for row in df.iterrows():
```

# 爬虫

## 自动处理cookie懒人方法

```
import requests
s = requests.Session()
s.headers = sina_header  # 这样处理一些参数
```


## webdriver自动化测试工具
强抵抗反爬虫版
```
import undetected_chromedriver as uc
driver = uc.Chrome()
```

# 图像与计算机视觉

## 截图
```
from PIL import ImageGrab

def window_capture(s, left,top,right,bottom):
    # (648, 320, 1272, 719)
    left = s[0] + left
    top = s[1] + top
    right = s[2] - right
    bottom = s[3] - bottom
    im = ImageGrab.grab((left,top,right,bottom))
    im.save('im.png')
    return im
```

## 验证码识别
```
import ddddocr
ocr = ddddocr.DdddOcr(show_ad = False)
```



# 性能测试工具
## cProfile

```
import cProfile
cProfile.run('enterance()')
```
## LineProfiler

```
from line_profiler import LineProfiler

lp = LineProfiler()
lp_wrapper = lp(mainroad)
lp_wrapper()
lp.print_stats()
```

# 程序性能优化：向量化计算 Numba 

https://numba.readthedocs.io/en/stable/user/5minguide.html

# 程序性能优化：多线程 多进程 并行开发

IO密集型程序，吃读写，应当采取多线程优化

CPU密集型程序，吃CPU计算，应当采取多进程优化

## 异步(asynchronous)开发

```
from multiprocessing import Pool
pool = Pool(jinchengshu)    # 线程
for config in config_list:
    pool.apply_async(main, (config,))
    # main(config)
pool.close()
pool.join()
```

https://docs.python.org/3.10/library/concurrent.futures.html

concurrent.futures同时提供了优于threading的开发方案

```
from concurrent.futures import ProcessPoolExecutor
with ProcessPoolExecutor(max_workers=config['进程数']) as pool:
    pool.submit(main, cfg)
```


