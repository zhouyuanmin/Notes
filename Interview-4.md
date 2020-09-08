---
title: Interview-4
date: 2020-01-28 12:37:40
tags:
- Interview
categories:
- Interview
keywords:
---

#### 单例

```python
# 简单案例
class A(object):
    _instance = None
    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = object.__new__(cls)
        return cls._instance
```

```python
# 应用场景
1. 资源共享：日志文件，应用配置
2. 资源控制：应用配置，日志文件，网站计数器，多线程池，数据库配置，数据库连接池
```

#### 闭包

```python
定义：在函数内部再定义一个函数，并且这个函数用到了外边函数的变量，那么将这个函数以及用到的一些变量称之为闭包。
```

#### 装饰器

```python
# 用于有切面需求的场景
# 插入日志、性能测试、事务处理、缓存、权限的校验等场景
# 有了装饰器就可以抽离出大量的与函数功能本身无关的雷同代码并发并继续使用
```

####  Python 中 is 和==的区别？

```python
is 通过id判断
== 通过value判断
```

#### 谈谈你对面向对象的理解？

```python
面向对象是相对于面向过程而言的。面向过程语言是一种基于功能分析的、以算法为中心的程序设计方法；
而面向对象是一种基于结构分析的、以数据为中心的程序设计思想。
在面向对象语言中有一个有很重要东西，叫做类。
面向对象有三大特性：封装、继承、多态。
```

