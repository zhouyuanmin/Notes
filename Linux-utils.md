---
title: Linux-utils
date: 2020-01-09 14:41:18
tags:
- Linux
categories:
- Linux
keywords:
- Linux-utils
---

#### axel

```shell
# 多线程下载工具-替代curl和wget
# 使用
axel -n 20 http://download.redis.io/releases/redis-5.0.7.tar.gz
```

#### lrzsz

```python
# 一款linux下命令行界面上支持上传和下载的第三方工具
rz  # 选择文件进行上传
sz 文件名  # sz后面跟文件名可以进行文件从linux上面下载
yum install -y lrzsz  # yum 安装完毕之后可以直接rz尝试使用
```

#### kill

```python
python3
import subprocess
import re
(status, output) = subprocess.getstatusoutput('ps -ef | grep python3')
subprocess.getstatusoutput('kill -9 {}'.format(' '.join(set(re.findall(r'\d{3,6}', output)))))
```

