---
title: Centos7-yum
date: 2020-01-09 12:04:59
tags:
- Linux
keywords:
categories:
- Linux
---

#### 安装源和更新

```shell
# 这操作很重要，可以避免很多版本性bug
yum install -y epel-release
yum update -y
```

#### 安装Python

```
yum install python36
```

#### 安装Redis

```
yum install redis
# 配置文件默认在/etc/redis.conf 
# 修改bind 127.0.0.1为0.0.0.0 修改port 6379为8888 修改protected-mode yes为no
# 修改 requirepass foobared 为自己的密码
# redis-server /etc/redis.conf  # 运行服务
# redis-cli -h 127.0.0.1 -p 8888 -a password  # 登录
# nohup redis-server /etc/redis.conf >/dev/null 2>&1 &  # 后台运行
```

```
编译安装redis链接：https://blog.csdn.net/qq_39185919/article/details/100564713
```

#### 安装Mongodb

```
# 1.创建仓库文件
vim /etc/yum.repos.d/mongodb-org-3.4.repo
添加如下内容
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
# 2.yum安装
yum install -y mongodb-org
# 3.修改配置文件，解除ip地址绑定信息
vim /etc/mongod.conf
修改为0.0.0.0 端口也修改为27027
# 启动，重启
systemctl start firewalld
systemctl start mongod
systemctl restart mongod
# 检查
cat /var/log/mongodb/mongod.log
mongo
```

```
# 卸载
yum erase $(rpm -qa | grep mongodb-org)
rm -r /var/log/mongodb
rm -r /var/lib/mongo
```

#### 安装mysql

```
https://blog.csdn.net/wohiusdashi/article/details/89358071
```

