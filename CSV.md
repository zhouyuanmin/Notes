---
title: CSV
date: 2020-03-17 01:16:00
tags:
- CSV
categories:
- CSV
keywords:
- CSV
- TranslationT
---

Translation

- 翻译官方文档-对应Python3.6
- *dialect* 方言，这里指定格式为 csv

#### 模块内容

- functions

```python
# csv.reader(csvfile, dialect='excel', **fmtparams)
# return: a list of strings
import csv
with open('eggs.csv', newline='') as csvfile:
    spamreader = csv.reader(csvfile, delimiter=' ', quotechar='|')
    for row in spamreader:
        print(', '.join(row))
```

```python
# csv.writer(csvfile, dialect='excel', **fmtparams)
# 写入是 a list of strings
import csv
with open('eggs.csv', 'w', newline='') as csvfile:
    spamwriter = csv.writer(csvfile, delimiter=' ',
                            quotechar='|', quoting=csv.QUOTE_MINIMAL)
    spamwriter.writerow(['Spam'] * 5 + ['Baked Beans'])
    spamwriter.writerow(['Spam', 'Lovely Spam', 'Wonderful Spam'])
```

- classes

```python
# csv.DictReader(f)
import csv
with open('names.csv', newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        print(row['first_name'], row['last_name'])
print(row)
# 公开接口
csvreader.__next__()  # 让对象变为 iterable object，使用next(reader) 
csvreader.dialect  # 只读
csvreader.line_num # 行数(包含首行目录), 这与返回的记录数不同，因为记录可以跨越多行。
csvreader.fieldnames # 目录（如果有，没有则是第一行）
```

```python
# csv.DictWriter(f)
import csv

with open('names.csv', 'w', newline='') as csvfile:
    fieldnames = ['first_name', 'last_name']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)  # 指定目录

    writer.writeheader()  # 写入目录
    writer.writerow({'first_name': 'Baked', 'last_name': 'Beans'})
    writer.writerow({'first_name': 'Lovely', 'last_name': 'Spam'})
    writer.writerow({'first_name': 'Wonderful', 'last_name': 'Spam'})
# 公开接口
csvwriter.writerow(row)
csvwriter.writerows(rows) # an iterable of row objects
DictWriter.writeheader()  # 写入目录（必须先在构造函数中指定）。
csvreader.dialect  # 只读
```

- exception

```python
csv.Error
# 所有异常都是Error
```

#### Dialects的默认参数

```python
# 一下参数了解，我们一般用不到，（不会去手动创建dialect对象）
Dialect.delimiter
# 分隔符，默认为 ','
Dialect.lineterminator
# 换行符 defaults '\r\n'
Dialect.strict
# When True, raise exception Error on bad CSV input. The default is False.
```

#### Examples

```python
import csv
with open('some.csv', newline='', encoding='utf-8') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
# 偶尔是 encoding='utf-8-sig' 
```

```python
import csv
for row in csv.reader(['one,two,three']): # 解析字符串
    print(row)
```

