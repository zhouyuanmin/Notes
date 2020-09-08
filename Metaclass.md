---
title: Metaclass
date: 2020-01-11 15:14:42
tags:
- Metaclass
categories:
- Metaclass
keywords:
- Metaclass
---

#### 元类

```python
Hello = type('Hello', (object,), dict(hello=fn))
```

#### 元类 metaclass

```python
# metaclass允许你创建类或者修改类
# 改变类创建时的行为
class ListMetaclass(type):
    def __new__(cls, name, bases, attrs):
        attrs['add'] = lambda self, value: self.append(value)
        return type.__new__(cls, name, bases, attrs)

class MyList(list, metaclass=ListMetaclass):
    pass
```

#### 常见的错误类型继承关系

[官方文档](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)

#### 多线程

[廖雪峰-多线程](https://www.liaoxuefeng.com/wiki/1016959663602400/1017629247922688)

