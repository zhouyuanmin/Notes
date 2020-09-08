---
title: OOP-Python
date: 2020-01-07 15:43:24
tags:
- OOP
categories:
- OOP
---

#### Technical Term

```
class 类
instance 实例
method 方法
subclass 子类
super class 父类
```

#### Method

```python
# 初始化
def __init__(self):
    pass
# 实例方法
def print_score(self):
    pass
# 类方法用@classmethod修饰，形参为cls
# 类实例方法，形参为self
# 静态方法用@staticmethod修饰，对象直接调用，实际上跟该类没有太大关系
```

#### Property

```python
# 实例属性
class Student(object):
    def __init__(self, name):
        self.name = name
# 类属性
class Student(object):
    name = 'Student'  
```

#### 限制实例的属性

```python
# 由于Python是动态语言，根据类创建的实例可以任意绑定属性
# 使用__slots__限制实例的属性
# __slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

#### 实例属性检查与暴露

```python
# @property装饰器：负责把一个方法变成属性调用
class Student(object):
    @property
    def score(self):
        return self._score
    @score.setter
    def score(self, value):
        pass
```

#### 多重继承

```
# C3算法：MRO(Method Resolution Order)方法解析顺序
# super()可以帮我们执⾏MRO中下⼀个⽗类的⽅法.
# MixIn设计模式（多重继承设计模式）
```

#### 定制类

```
# __len__(self) 与 len()
# __str__(self) 与 print()打印  # __repr__(self)
# __iter__(self) 和 __next__(self)
# __getitem__(self, n) # fib[12]和fib[5:12]
# __delitem__(self, key)  # 与__setitem__(self,name,value)类似，每次都调用
```

```python
# __setitem__(self,name,value)
class A:
    def __init__(self):
        self['B'] = 'BB'
        self['D'] = 'DD'

    def __setitem__(self, name, value):
        print("__setitem__:Set %s Value %s" % (name, value))


if __name__ == '__main__':
    X = A()
# 输出结果如下
# __setitem__:Set B Value BB
# __setitem__:Set D Value DD
```

```
# __getattr__(self, attr)  # 动态返回属性attr
# 链式调用，SDK的API常用
# __call__(self, name)  # 直接调用
```

```python
class Chain(object):
    def __init__(self, path=''):
        self._path = path

    def __getattr__(self, path):
        return Chain('%s/%s' % (self._path, path))

    def __str__(self):
        return self._path

    def __call__(self, user):
        return Chain(self.__getattr__(user))

    __repr__ = __str__


print(Chain().status.user.timeline.list)
# 输出: /status/user/timeline/list
print(Chain().users('Jason').repos)
# 输出: /users/Jason/repos
```

```python
# 何动态获取和设置对象的属性 has,get,set > attr
if hasattr(Parent，'x'):
    print(getattr(Parent, 'x'))
    setattr(Parent, 'x', 3)
print(getattr(Parent, 'x'))
```

[未完，待补充]()

