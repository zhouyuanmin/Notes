---
title: Map-reduce-filter
date: 2020-01-07 13:11:41
tags:
categories:
- Python
---

#### map

```
把func作用在iterator每一个元素上，并返回一个iterator
```

#### reduce

```
累积计算  # func(x,y)必须两个参数
```

#### filter

```
过滤函数 
# 把func作用在iterator每一个元素上，然后根据返回值是Ture还是False决定保留还是丢弃该元素
# 返回值是原来iterator的子序列
```

#### 注意

```
map、reduce、filter都是两个参数（第一个func，第二个iterator）
返回值都是惰性iterator，需要list()才能转换为list
```

