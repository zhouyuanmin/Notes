---
title: Logging
date: 2020-02-23 02:25:02
tags:
- Python
categories:
- Python
keywords:
---

#### 日志级别

```python
import logging
logging.debug("Hello")
logging.info("Hello")
logging.warning("Hello") # 默认
logging.error("Hello")
logging.critical("Hello")
```

#### 控制级别

```python
import logging
logging.basicConfig(level=logging.NOTSET)  # 设置日志级别
```

#### 控制日志格式

```python
logging.basicConfig(level=logging.DEBUG,
             format='[%(levelname)s][%(asctime)s][%(filename)s][%(message)s]')
# 推荐格式'[%(levelname)s][%(asctime)s][%(filename)s][%(message)s]'
```

#### 基本操作流程（经典案例）

```python
import logging
import os

logger = logging.getLogger()
logger.setLevel(logging.DEBUG)  # 设置为最低

log_dir = os.path.join(os.getcwd(), 'Logs')
log_file = os.path.join(log_dir, 'spider_error.log')
if not os.path.exists(log_dir):
    os.mkdir(log_dir)

file_handler = logging.FileHandler(log_file, mode='a')  # 日志文件
file_handler.setLevel(logging.ERROR)
file_handler.setFormatter(logging.Formatter('[%(levelname)s][%(asctime)s][%(message)s]'))
logger.addHandler(file_handler)

console_handler = logging.StreamHandler()  # 控制台
console_handler.setLevel(logging.INFO)
console_handler.setFormatter(logging.Formatter('[%(levelname)s][%(asctime)s][%(message)s]'))
logger.addHandler(console_handler)
# 所有日志都到logger里面,需要输出到哪里，就过滤，拷贝到哪里。
```

[logging参考连接](https://www.cnblogs.com/CJOKER/p/8295272.html)

