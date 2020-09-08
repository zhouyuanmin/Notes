# Python标准数据结构

### 一、数字 Number

##### 1.支持类型

- int、float、complex 

##### 2.转换

- int(x) , float(x) , complex(x[,y])

##### 3.整数表示

- 0xA1 , 0o241 , 161 ,  0b10100001
- hex() , otc() , int() , bin()

##### 4.补充

- / 和 // 区分

##### 5.数学函数

- abs(-10) 返回绝对值
- math.ceil(4.1) 向上取整
- math.floor(4.9) 向下取整
- round(2.675, 2) 四舍五入，保留两位

### 二、字符串 String

##### 1.常用方法

- .capitalize() 第一个字符转换为大写
- .count(str, beg= 0,end=len(string)) 计数，beg和end是index范围
- .decode()和.encode()
- .find(str, beg= 0,end=len(string))  返回index或者-1
- .isalnum()  都是字母或者数字
- .isalpha() 都是字母
- .isdigit()  都是数字
- .islower() 和 .isupper() 都是小写或者大写
- .join(seq) 合并
- .lower() 转小写， upper()  转大写
- .replace(old, new [, max])  替换
- .strip() , .lstrip() , .rstrip()  删除左右空格
- .split(str="", num=string.count(str))  分隔成list

##### 2.格式化输出

- **:** 号后面带填充的字符，只能是一个字符，不指定则默认是用空格填充。
- **^**, **<**, **>** 分别是居中、左对齐、右对齐，后面带宽度，如 {:>10d}
- **+** 表示在正数前显示 **+**，负数前显示 **-**
- b、d、o、x 分别是二进制、十进制、八进制、十六进制。
- . 右边是保留小数位数，左边则是总位数。print("{:#>13.3f}".format(2022220.22222))

### 三、列表 List

##### 1.常用方法

- .append()
- .count()
- .extend()  追加seq
- .index()
- .insert()
- .pop()
- .remove(obj)  移除第一个匹配项
- .reverse()  反转列表（原list）
- .sort(key=None,reverse=False)  排序
- .clear()
- .copy()

##### 2.补充

- list()

### 四、元组 Tuple

##### 1.补充

- tuple(iterable)

### 五、集合 Set

##### 1.常用方法

- .add()
- .update(x [,x])   添加, x 可以多个, x 可以为 list, set, dict
- .remove( x ) 推荐使用 .discard( x ) 不会报错
- .pop()  随机删除一个
- .clear()

##### 2.补充

- x in set
- 两个set操作有 **- | & ^**

### 六、字典 Dictionary

##### 1.常用方法

- .clear()
- .copy()
- .get(key, default=None)
- items()  和  keys()  和  values()
- setdefault(key,default=None)  其他部分等价于 get()
- .update(dict2)
- pop(key [,default])
- popitem()

##### 2.补充

- len(dict)
- str(dict)
- key in dict

