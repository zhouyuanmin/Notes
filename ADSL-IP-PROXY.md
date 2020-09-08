---
title: ADSL-IP-PROXY
date: 2020-01-03 11:19:07
tags:
- Spider
categories:
- Spider
---

### 1.介绍

```
使用vps服务器搭建IP代理池（高匿名）
```

### 2.准备工作

```ｐｙｔｈｏｎ
１、购买VPS主机（多台，至少两台），并预装centos7
２、一台正常服务器（也可以再购买一台VPS主机）
```

### 3.搭建代理服务器

```python
# 3.1 登录VPS服务器
ssh root@58.218.209.207 -p 20113   # 密码在“控制面版”
```

```python
# 3.2 拨号-先拨号才可以连接外网
adsl-start  # 此命令是拨号
adsl-stop   # 此命令是停止拨号
```

```python
# 3.3 查看主机的IP
ifconfig
# 网卡名称叫ppp0,他的ip地址就是
```

```python
# 3.4安装代理服务器TinyProxy
yum install -y epel-release
yum update -y
yum install -y tinyproxy
```

```python
# 3.5 配置TinyProxy
vim /etc/tinyproxy/tinyproxy.conf
# 里面有一行是 Port 8888，这是代理端口，默认不修改
# 里面有一行是 Allow 127.0.0.1 ，将它注释掉，即可任何主机使用本代理服务器
# 设置完成之后，需要重启TinyProxy
systemctl enable tinyproxy.service
systemctl restart tinyproxy.service
```

```python
# 3.6 开放防火墙端口
iptables -I INPUT -p tcp --dport 8888 -j ACCEPT
# 或者直接关闭防火墙
systemctl stop firewall.service
```

```python
# 3.7 验证TinyProxy
# 在其他主机输入curl命令
curl -x 112.84.118.216:8888 httpbin.org/get
# 返回的“origin”是代理服务器即为成功
```

### 4.搭建代理池

```python
# 4.1 存储模块：使用Redis数据库，存储各个代理服务器的代理ip和代理端口（正常服务器上）
# 先定义一个操作 Redis 数据库的类，示例如下：
```

```python
import redis
import random

# Redis 数据库 IP
REDIS_HOST = 'remoteaddress'
# Redis 数据库密码，如无则填 None
REDIS_PASSWORD = 'password'
# Redis 数据库端口
REDIS_PORT = 6379
# 代理池键名
PROXY_KEY = 'adsl'

class RedisClient(object):
    def __init__(self, host=REDIS_HOST, port=REDIS_PORT, password=REDIS_PASSWORD, proxy_key=PROXY_KEY):
        """
        初始化 Redis 连接
        :param host: Redis 地址
        :param port: Redis 端口
        :param password: Redis 密码
        :param proxy_key: Redis 哈希表名
        """
        self.db = redis.StrictRedis(host=host, port=port, password=password, decode_responses=True)
        self.proxy_key = proxy_key

    def set(self, name, proxy):
        """
        设置代理
        :param name: 主机名称
        :param proxy: 代理
        :return: 设置结果
        """
        return self.db.hset(self.proxy_key, name, proxy)

    def get(self, name):
        """
        获取代理
        :param name: 主机名称
        :return: 代理
        """
        return self.db.hget(self.proxy_key, name)

    def count(self):
        """
        获取代理总数
        :return: 代理总数
        """
        return self.db.hlen(self.proxy_key)

    def remove(self, name):
        """
        删除代理
        :param name: 主机名称
        :return: 删除结果
        """
        return self.db.hdel(self.proxy_key, name)

    def names(self):
        """
        获取主机名称列表
        :return: 获取主机名称列表
        """
        return self.db.hkeys(self.proxy_key)

    def proxies(self):
        """
        获取代理列表
        :return: 代理列表
        """
        return self.db.hvals(self.proxy_key)

    def random(self):
        """
        随机获取代理
        :return:
        """
        proxies = self.proxies()
        return random.choice(proxies)

    def all(self):
        """
        获取字典
        :return:
        """return self.db.hgetall(self.proxy_key)
```

```python
# 4.2 拨号模块：拨号，并把新的 IP 保存到 Redis 散列表里（本模块在vps拨号服务器上）
```

```python
import re
import time
import requests
from requests.exceptions import ConnectionError, ReadTimeout
from db import RedisClient
 
# 拨号网卡
ADSL_IFNAME = 'ppp0'
# 测试 URL
TEST_URL = 'http://www.baidu.com'
# 测试超时时间
TEST_TIMEOUT = 20
# 拨号间隔
ADSL_CYCLE = 100
# 拨号出错重试间隔
ADSL_ERROR_CYCLE = 5
# ADSL 命令
ADSL_BASH = 'adsl-stop;adsl-start'
# 代理运行端口
PROXY_PORT = 8888
# 客户端唯一标识
CLIENT_NAME = 'adsl1'
 
class Sender():
    def get_ip(self, ifname=ADSL_IFNAME):
        """
        获取本机 IP
        :param ifname: 网卡名称
        :return:
        """
        (status, output) = subprocess.getstatusoutput('ifconfig')
        if status == 0:
            pattern = re.compile(ifname + '.*?inet.*?(d+.d+.d+.d+).*?netmask', re.S)
            result = re.search(pattern, output)
            if result:
                ip = result.group(1)
                return ip
 
    def test_proxy(self, proxy):
        """
        测试代理
        :param proxy: 代理
        :return: 测试结果
        """
        try:
            response = requests.get(TEST_URL, proxies={
                'http': 'http://' + proxy,
                'https': 'https://' + proxy
            }, timeout=TEST_TIMEOUT)
            if response.status_code == 200:
                return True
        except (ConnectionError, ReadTimeout):
            return False
 
    def remove_proxy(self):
        """
        移除代理
        :return: None
        """
        self.redis = RedisClient()
        self.redis.remove(CLIENT_NAME)
        print('Successfully Removed Proxy')
 
    def set_proxy(self, proxy):
        """
        设置代理
        :param proxy: 代理
        :return: None
        """
        self.redis = RedisClient()
        if self.redis.set(CLIENT_NAME, proxy):
            print('Successfully Set Proxy', proxy)
 
    def adsl(self):
        """
        拨号主进程
        :return: None
        """
        while True:
            print('ADSL Start, Remove Proxy, Please wait')
            self.remove_proxy()
            (status, output) = subprocess.getstatusoutput(ADSL_BASH)
            if status == 0:
                print('ADSL Successfully')
                ip = self.get_ip()
                if ip:
                    print('Now IP', ip)
                    print('Testing Proxy, Please Wait')
                    proxy = '{ip}:{port}'.format(ip=ip, port=PROXY_PORT)
                    if self.test_proxy(proxy):
                        print('Valid Proxy')
                        self.set_proxy(proxy)
                        print('Sleeping')
                        time.sleep(ADSL_CYCLE)
                    else:
                        print('Invalid Proxy')
                else:
                    print('Get IP Failed, Re Dialing')
                    time.sleep(ADSL_ERROR_CYCLE)
            else:
                print('ADSL Failed, Please Check')
                time.sleep(ADSL_ERROR_CYCLE)
def run():
    sender = Sender()
    sender.adsl()
```

```python
# 4.3 接口模块（正常服务器上）
# 利用 Tornado 的 Server 模块搭建 Web 接口服务
```

```python
import json
import tornado.ioloop
import tornado.web
from tornado.web import RequestHandler, Application
 
# API 端口
API_PORT = 8000
 
class MainHandler(RequestHandler):
    def initialize(self, redis):
        self.redis = redis
 
    def get(self, api=''):
        if not api:
            links = ['random', 'proxies', 'names', 'all', 'count']
            self.write('<h4>Welcome to ADSL Proxy API</h4>')
            for link in links:
                self.write('<a href=' + link + '>' + link + '</a><br>')
 
        if api == 'random':
            result = self.redis.random()
            if result:
                self.write(result)
 
        if api == 'names':
            result = self.redis.names()
            if result:
                self.write(json.dumps(result))
 
        if api == 'proxies':
            result = self.redis.proxies()
            if result:
                self.write(json.dumps(result))
 
        if api == 'all':
            result = self.redis.all()
            if result:
                self.write(json.dumps(result))
 
        if api == 'count':
            self.write(str(self.redis.count()))
 
def server(redis, port=API_PORT, address=''):
    application = Application([(r'/', MainHandler, dict(redis=redis)),
        (r'/(.*)', MainHandler, dict(redis=redis)),
    ])
    application.listen(port, address=address)
    print('ADSL API Listening on', port)
    tornado.ioloop.IOLoop.instance().start()
```

### 程序转后台运行命令

```shell
# vps server
nohup python3  run.py >/dev/null 2>&1 &
# redis server
nohup python3 api.py >/dev/null 2>&1 &
```

```shell
# 查询存活程序python3
ps -ef | grep python3
```

### 参考链接

[崔老师-ADSL 拨号代理](https://cuiqingcai.com/8361.html)

[github项目链接](https://github.com/squabbysheep/AdslProxy)

### 实例链接

[ADSL实例](http://121.36.55.134:80/)

