---
title: Function-param
date: 2020-01-06 14:01:32
tags:
categories:
- Python
---

#### 1.位置参数

```python
def power(x):
	return x*x
```

#### 2.默认参数

```python
def power(x=1):
	return x*x
# 必选参数在前，默认参数在后
# 变化大的参数在前，变化小的参数在后
# 变化小的参数可以作为默认参数
```

#### 3.可变参数

```python
def cale(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

cale(1,2,3)
```

#### 4.关键字参数

```python
def person(name, age, **kw)
    print('name:',name,'age:',age,'other',kw)
person('Tom', 30)
person('Tom', 30, city='beijing')
person('Tom', 30, **dict1)
```

#### 5.命名关键字参数

```python
def person(name,age,*,city,job):
    # 没有可变参数时
    pass
def person1(name,age,*args,city='beijing',job):
    # 有可变参数时，不再需要特殊分隔符*
    pass
```

#### 参数组合

```
顺序：必选参数（位置参数），默认参数，可变参数，关键字参数，命名关键字参数
```

#### 备注

```
func(*args,**kw)
对于任意函数，都可以通过类似func(*args,**kw)的形式调用它，无论它的参数是如何定义的。
```

