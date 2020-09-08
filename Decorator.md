---
title: Decorator
date: 2020-01-07 13:45:00
tags:
- Decorator
categories:
- Python
---

### 装饰器（装饰模式）

#### 例子1

```python
# 两层
def log(func):
    def wrapper(*args, **kw):
        print('log')
        return func(*args, **kw)
    return wrapper
@log
def test():
    print('test')
```

#### 例子2

```python
# 三层：针对decorator有参数的时候
def log(text):
    def decorater(func):
        def wrapper(*args, **kw):
            print('log:', text)
            return func(*args, **kw)

        return wrapper

    return decorater


@log('text')
def test():
    print('test')
```

#### 备注

```python
import functools
@functools.wraps(func)  # 将函数func的一些特殊属性复制给wrapper函数（最里层函数）
```

