---
title: Interview-3
date: 2020-01-27 23:06:10
tags:
- Interview
categories:
- Interview
keywords:
---

### Python 的内存管理机制及调优手段？

```python
# 内存管理机制：引用计数、垃圾回收、内存池
```

```python
# 1.引用计数
当一个 Python 对象被引用时，引用计数加1，
当不再被一个变量，减1，
当引用计数等于0时对象被删除。
```

```python
# 2.垃圾回收
2.1 引用计数
当引用计数为0,则被回收 （对循环引用，失效）
2.2 标记清除 
针对循环引用，先将循环引用摘掉，得出有效计数
2.3 分代回收
```

```python
# 3. 内存池
用于管理对小块内存的申请和释放（小于256字节的，直接在内存池申请内存）
```

```python
调优手段（了解）
1.手动垃圾回收
2.调高垃圾回收阈值
3.避免循环引用（手动解循环引用和使用弱引用）
```

### 内存泄露是什么？如何避免？

```python
# 由于设计错误，失去对该段内存的控制，造成内存浪费。
# 有 __del__() 函数的对象间的循环引用是导致内存泄漏的主凶
```

```python
# 避免
不使用一个对象时使用 del object 删除一个引用计数
可以通过 sys.getrefcount(obj) 获取对象的引用计数，根据返回值是否为 0 判断是否内存泄漏
```
