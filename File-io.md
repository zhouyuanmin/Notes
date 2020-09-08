---
title: File-io
date: 2020-01-27 15:15:17
tags:
- Interview
categories:
- Interview
keywords:
- IO
---

#### 4G 内存怎么读取一个 5G 的数据？

```python
# 方法一:
# 生成器，分多次读取
def my_read(file, separator):  # 流对象，分隔符
    buffer = ""
    while True:
        while separator in buffer:  # 此处while比if更合适, 处理buffer有多个separator
            pos = buffer.index(separator)  # 获取第一个下标
            yield separator[:pos]
            buffer = buffer[pos + len(separator):]
        chunk = file.read(2000)  # 太小也会降低效率
        if not chunk:
            yield buffer
            break
        buffer = buffer + chunk

with open('f.txt', 'r') as f:
    for line in my_read(f, separator='\n'):
        print(line)
```

```python
# 方法二:
# linux命令split切割成小文件
split -l 300 big.txt -d -a 4 big_  # 系数不是字母而是数字（-d），后缀系数为四位数（-a 4）
split -b 10m big.txt big_          # 按照大小切割
```

- [linux命令split切割成小文件](https://blog.csdn.net/mxgsgtc/article/details/12048919)

