---
title: Python-call-C
date: 2020-01-03 12:19:08
tags:
- C&C++
categories:
- C&C++
---

### Python3 调用C语言代码

##### 开发环境

```
centos7+python3.6
```

##### 备注

```
Python中的ctypes模块可能是Python调用C方法中最简单的一种。
ctypes模块提供了和C语言兼容的数据类型和函数来加载dll文件，
因此在调用时不需对源文件做任何的修改，也正是如此奠定了这种方法的简单性。
```

##### 准备文件

###### 1.准备C语言程序，保存为add.c

```c
#include <stdio.h>

int add_int(int, int);
float add_float(float, float);
 
int add_int(int num1, int num2){
    return num1 + num2;
}
 
float add_float(float num1, float num2){
    return num1 + num2;
}
```

###### 2.编译成so库

输入命令即可，会出现一个.so文件

```
gcc -shared -Wl,-soname,adder -o adder.so -fPIC add.c
```

###### 3.准备python代码，保存为python-c.py

```python
import ctypes
 
#load the shared object file
adder = ctypes.cdll.LoadLibrary('./adder.so')
 
#Find sum of integers
res_int = adder.add_int(4,5)
print("4 + 5 = " + str(res_int))
 
#Find sum of floats
a = ctypes.c_float(5.5)
b = ctypes.c_float(4.1)
 
add_float = adder.add_float
add_float.restype = ctypes.c_float
 
print("5.5 + 4.1 = " + str(add_float(a, b)))
```

###### 4.执行

```
python3 python-c.py
```

执行结果如下

```
4 + 5 = 9
5.5 + 4.1 = 9.600000381469727
```

###### 5.特殊说明

- 在Python文件中，一开始先导入ctypes模块，然后使用cdll.LoadLibrary函数来加载我们创建的库文件。这样我们就可以通过变量adder来使用C类库中的函数了。当adder.add_int()被调用时，内部将发起一个对C函数add_int的调用。ctypes接口允许我们在调用C函数时使用原生Python中默认的字符串型和整型。
- 而对于其他类似布尔型和浮点型这样的类型，必须要使用正确的ctype类型才可以。如向adder.add_float()函数传参时, 我们要先将Python中的十进制值转化为c_float类型，然后才能传送给C函数。这种方法虽然简单，清晰，但是却很受限。例如，并不能在C中对对象进行操作。