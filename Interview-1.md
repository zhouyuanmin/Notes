---
title: Interview-1
date: 2020-01-21 12:45:14
tags:
- Interview
categories:
- Interview
keywords:
- Interview
---

```python
修改不可变数据会抛出TypeError异常
```

```python
print 方法默认调用 sys.stdout.write 方法
```

```python
# 文件路径操作
def print_directory_contents(abs_path):
    """
    :param abs_path: 文件夹绝对地址
    :return: 该文件夹中文件路径+包含的文件夹的文件路径
    """
    import os
    for child_path in os.listdir(abs_path):
        abs_child_path = os.path.join(abs_path, child_path)
        if os.path.isdir(abs_child_path):
            print_directory_contents(abs_child_path)
        else:
            print(abs_child_path)
'''
os.remove()删除文件
os.rename()重命名文件
os.walk()生成目录树下的所有文件名
os.chdir()改变目录
os.mkdir/makedirs 创建目录/多层目录
os.rmdir/removedirs 删除目录/多层目录
os.listdir()列出指定目录的文件
os.getcwd()取得当前工作目录
os.chmod()改变目录权限
os.path.basename()去掉目录路径，返回文件名
os.path.dirname()去掉文件名，返回目录路径
os.path.join()将分离的各部分组合成一个路径名
os.path.split()返回（dirname(),basename())元组
os.path.splitext()(返回 filename,extension)元组
os.path.getatime\ctime\mtime 分别返回最近访问、创建、修改时间
os.path.getsize()返回文件大小
os.path.exists()是否存在
os.path.isabs()是否为绝对路径
os.path.isdir()是否为目录
os.path.isfile()是否为文件
'''
```

```python
# 拷贝
import copy
copy.deepcopy(a)  # 深拷贝
# '原子'类型的对象拷贝,都是返回引用,不是新创建
```

```python
# random模块
import random
random.random()  # [0,1) float
random.uniform(a, b)  # [a,b] float
random.randint(a, b)  # [a,b] int
random.randrange(a, b, step)  # [a,b) step为步长，随机一个数字
random.choice(sequence)  # list中随机一个元素
random.shuffle(alist)  # 打乱顺序，无返回值
```

```python
# datetime
import datetime
date1 = datetime.date(year=int(100),month=int(2),day=int(22))
print((date1-date1).days + 1)
```

```python
# sys模块
sys.path 主要是对 Python 解释器的系统环境参数的操作（动态的改变 Python 解释器搜索路径）
sys.argv 命令行参数 List，第一个元素是程序本身代码（即此.py程序）# 有时候带路径
sys.exit(n) 退出程序，正常退出时 exit(0)
sys.maxint 最大的 Int 值
sys.maxunicode 最大的 Unicode 值
sys.stdout 标准输出
sys.stdin 标准输入
sys.stderr 错误输出
```

```python
# Python 是强语言类型还是弱语言类型?
Python 是强类型的动态脚本语言。  # 强类型
强类型：不允许不同类型相加。
动态：不使用显示数据类型声明，且确定一个变量的类型是在第一次给它赋值的时候。
脚本语言：一般也是解释型语言，运行代码只需要一个解释器，不需要编译。
```

[Python自省 (introspection)](https://www.woola.net/detail/2016-08-28-python-object-introspection.html)

```python
# PEP8 规范
# 模块和包:除特殊模块 __init__ 之外，模块名称都使用不带下划线的小写字母。若是它们实现一个协议，那么通常使用lib为后缀
# 使用 has 或 is 前缀命名布尔元素 is_connect = True  has_member = False
```

```python
# 性能分析
import cProfile
cProfile.run('func(agrs)')   # 字符串
```

