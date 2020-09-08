---
title: Pip
date: 2020-03-17 16:00:09
tags:
- Pip
categories:
- Pip
keywords:
---

#### 设置pip源

```
cd  # 回到家目录
mkdir .pip
vim .pip/pip.conf
写入如下内容
[global]
timeout = 6000
index-url = http://pypi.douban.com/simple
trusted-host = pypi.douban.com
```

```
一、在windows环境下修改pip镜像源的方法(以python3.5为例)
(1):在windows文件管理器中,输入 %APPDATA%
(2):会定位到一个新的目录下，在该目录下新建pip文件夹，然后到pip文件夹里面去新建个pip.ini文件
(3):在新建的pip.ini文件中输入以下内容，搞定文件路径："C:\Users\Administrator\AppData\Roaming\pip\pip.ini"
[global]
timeout = 6000
index-url = http://pypi.douban.com/simple
trusted-host = pypi.douban.com
```

