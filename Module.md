---
title: Module
date: 2020-01-07 14:35:32
tags:
categories:
- Python
---

### 介绍模块相关一些小知识

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Jason '

import sys

def test():
    args = sys.argv   # 命令行参数，第一个默认为文件名
    if len(args)==1:
        print('Hello, world!')
    elif len(args)==2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')

if __name__=='__main__':
    test()
```

```python
#!/usr/bin/env python3
可以让文件直接在Unix/Linux/Mac上运行
```

```
# -*- coding: utf-8 -*-
统一使用标准utf-8编码
```

```
任何模块代码的第一个字符串都被视为模块的文档注释
```

```
__author__变量是作者
```

### 模块搜索路径

```python
import sys
sys.path.append('模块路径')
# 这种方法是在运行时修改（添加），运行结束后失效
```



