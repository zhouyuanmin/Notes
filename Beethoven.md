---
title: Beethoven
date: 2020-01-15 19:26:30 
tags:
- Beethoven
categories:
- Beethoven
keywords:
- Beethoven
---

#### os

```python
import os
os.getpid()
os.getppid()
```

#### multiprocessing

```python
# 部署分布式（master）
import queue
task_queue = queue.Queue()  # 队列，后面会通过BaseManager封装，注册到网络上
from multiprocessing.managers import BaseManager
class QueueManager(BaseManager):
    pass
QueueManager.register('get_task_queue', callable=lambda: task_queue)  # 必须注册
manager = QueueManager(address=('', 5000), authkey=b'abc')
task = manager.get_task_queue()  # 获取队列queue
manager.start()  # 开启
manager.shutdown()  # 关闭
# slave
class QueueManager(BaseManager):
    pass
QueueManager.register('get_task_queue')  # 一定要注册
m = QueueManager(address=(master_ip, 5000), authkey=b'abc')
m.connect()
task = m.get_task_queue()
```

#### threading

```python
import threading
threading.current_thread().name
from threading import Thread
from threading import Lock
from threading import local
```

#### datetime

```python
from datetime import datetime
now = datetime.now()
now.timestamp() # 时间戳
datetime.fromtimestamp(1429417200.0)
datetime.utcfromtimestamp(1429417200.0)
now.strftime('%Y-%m-%d %H:%M:%S %A')
from datetime import timedelta
datetime.now() + timedelta(days=2, hours=12)
# 设置时区
from datetime import timezone
now.replace(tzinfo=timezone(timedelta(hours=8)))
```

#### collections

```python
# 具名元组
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)  # 使用 p.x
# 队列，等价于list；更高效
from collections import deque
# 默认字典，等价于dict；key不存在，返回默认值，不报错
from collections import defaultdict
dd = defaultdict(lambda: 'N/A')
# 有序字典
from collections import OrderedDict
od = OrderedDict([('a', 1), ('b', 2), ('c', 3)])
# ChainMap
from collections import ChainMap
```

#### ChainMap

```python
from collections import ChainMap
combined = ChainMap(dict1, dict2, defaults)   # 链式dict
```

#### Counter

```python
from collections import Counter
# 计数器
c = Counter()
c.update('hello')
```

#### base64

```python
import base64
base64.b64encode(b"abcde")   # b'YWJjZGU='  编码
base64.b64decode(b'YWJjZGU=')     # b'abcde'   解码
# Base64是一种任意二进制到文本字符串的编码方法，常用于在URL、Cookie、网页中传输少量二进制数据
```

#### struct

```python
import struct
# 转化为bytes
struct.pack('>I',10240099)   # b'\x00\x9c@c'
# 转化为python数据
struct.unpack('>IH', b'\xf0\xf0\xf0\xf0\x80\x80')   # (4042322160, 32896)
# 
I：4字节无符号整数,即unsigned int
H：2字节无符号整数,即unsigned short
c: char
```

#### hashlib

```python
import hashlib
md5 = hashlib.md5()   #
md5.update("date".encode('utf-8'))
md5.hexdigest()
# 补充
hashlib.sha1()
# md5:128 bit字节,32位16进制
# sha1: 160 bit, 40位16进制
单向计算特性决定了其作用是防篡改，不能用于加密（不能反推明文）
```

#### hmac

```python
import hmac
h = hmac.new(key=b'key', msg=None, digestmod='MD5')
h.update(msg=b'msg')
h.hexdigest()
```

#### itertools

```python
import itertools
itertools.count(start=0, step=1)  # 无限迭代器
itertools.cycle('ABC')  # iterable 无限重复
itertools.repeat(object [,times])
itertools.takewhile(lambda x: x <= 10, natuals) 
itertools.chain(*iterables)  # 合并成一个迭代器
```

#### contextlib

- 上下文管理

```python
class Test(object):
    def __init__(self, name):
        self.name = name
    def __enter__(self):
        return self   # 非常重要，一定要返回一个对象，一般返回self
    def __exit__(self, exc_type, exc_value, traceback):
        if exc_type:
            print("ERROR处理")
        else:
            print("NO ERROR")
    def test(self):
        print("this is a test class.it is {}".format(self.name))

with Test('Bob') as f:
    f.test()
```

```python
# @contextmanager用法一
from contextlib import contextmanager
class Query(object):
    def __init__(self, name):
        self.name = name
    def query(self):
        print('Query info about %s...' % self.name)
@contextmanager
def create_query(name):
    print('Begin')
    q = Query(name)
    yield q
    print('End')
with create_query('Bob') as q:
    q.query()
# 用法二
@contextmanager
def tag(name):
    print("<%s>" % name)
    yield
    print("</%s>" % name)
with tag("h1"):
    print("hello")
    print("world")
```

#### Pillow

```python
from PIL import Image
im = Image.open('test.jpg')  # 读取图片
w, h = im.size   # 图像尺寸
im.thumbnail((w//2, h//2))   # 缩小
im.save('thumbnail.jpg', 'jpeg')  # 保存
```

```python
from PIL import Image, ImageDraw, ImageFont
# 生成验证码
# 图片大小，字体类型，字内容，字大小，字
image = Image.new('RGB', (60 * 4, 60), (255, 255, 255))  # 创建图片
draw = ImageDraw.Draw(image)  # 操作对象
draw.point((50, 50), fill=(100, 100, 100))  # 修改一个像素点
font = ImageFont.truetype('Arial.ttf', 36)  # 指定字体类型和大小
draw.text((60, 10), "A", font=font, fill=(90, 90, 90))  # 写入一个“A”
image.save('code.jpg', 'jpeg')
```

#### chardet

```python
# 猜测bytes到str,的编码规则：utf8,ascii等各种编码格式，包括日语韩语等
chardet.detect(b'Hello, world!')
```

#### psutil

```python
# 运维
import psutil
psutil.cpu_count()  # CPU逻辑数量 4个
psutil.cpu_count(logical=False)  # CPU物理核心 2个
# 2说明是双核超线程(1个物理核心对应2个逻辑), 4则是4核非超线程
```

[psutil-example](https://github.com/giampaolo/psutil#example-usages)

#### virtualenv

```shell
pip install virtualenv
mkdir myproject
cd myproject/
# 创建一个独立的Python运行环境，命名为venv
virtualenv --no-site-packages venv    # 会出现文件夹venv
virtualenv -p /usr/bin/python2.7 venv
–no-site-packages  # 令隔离环境不能访问系统全局的site-packages目录。（好像不能用了）
–system-site-packages # 令隔离环境可以访问系统全局的site-packages目录。
source venv/bin/activate  # 进入该环境，成功命令提示符前面会出现(venv)
deactivate  # 退出该环境
```