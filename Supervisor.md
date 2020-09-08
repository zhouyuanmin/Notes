---
title: Supervisor
date: 2020-01-08 13:33:52
tags:
- Linux
categories:
- Linux
---

### Supervisor

#### 专业名称解释

```python
supervisor：要安装的软件的名称。
supervisord：装好supervisor软件后，supervisord用于启动supervisor服务。
supervisorctl：用于管理supervisor配置文件中program。
```

#### 环境

- centos7

#### 安装

```python
yum install epel-release
yum install -y supervisor
systemctl enable supervisord # 开机自启动
systemctl start supervisord # 启动supervisord服务
systemctl status supervisord # 查看supervisord服务状态
ps -ef|grep supervisord # 查看是否存在supervisord进程
```

```
# 可以看到配置文件位置
# 主配置文件在/etc/supervisord.conf
# 子配置文件放在/etc/supervisord.d目录里面  # 以.ini结束的配置文件
```

#### 配置为supervisor服务

```python
vim /usr/lib/systemd/system/supervisord.service
# 将下面一段配置信息粘贴进去(类似/usr/bin/supervisord的路径需要自己修改对应的)
```

```python
[Unit]
Description=Process Monitoring and Control Daemon
After=rc-local.service nss-user-lookup.target

[Service]
Type=forking
PIDFile=/var/run/supervisord.pid
ExecStart=/usr/bin/supervisord -c /etc/supervisord.conf
ExecStop=/usr/bin/supervisorctl shutdown
ExecReload=/usr/bin/supervisorctl reload
KillMode=process
Restart=on-failure   # 非正常退出，会重启
RestartSec=42s   # 重启之前等待42秒

[Install]
WantedBy=multi-user.target
```

```python
启动服务
systemctl enable supervisord
检查是否启动成功
systemctl is-enabled supervisord  # 出现enabled，则启动成功
```

```python
# 可以使用如下命令管理supervisor服务了
systemctl stop supervisord
systemctl start supervisord
systemctl status supervisord
systemctl reload supervisord
systemctl restart supervisord
```

### supervisor简单使用

#### 开放到外网

```python
port=*:9001                ;Web管理后台运行的IP和端口，如果开放到公网，需要注意安全性
username=user              ;登录管理后台的用户名
password=123               ;登录管理后台的密码
```

#### 子进程配置

- 讲解

```python
#项目名
[program:blog]
#脚本目录
directory=/opt/bin
#脚本执行命令
command=/usr/bin/python /opt/bin/test.py

#supervisor启动的时候是否随着同时启动，默认True
autostart=true
#当程序exit的时候，这个program不会自动重启,默认unexpected，设置子进程挂掉后自动重启的情况，有三个选项，false,unexpected和true。如果为false的时候，无论什么情况下，都不会被重新启动，如果为unexpected，只有当进程的退出码不在下面的exitcodes里面定义的
autorestart=false
#这个选项是子进程启动多少秒之后，此时状态如果是running，则我们认为启动成功了。默认值为1
startsecs=1

#脚本运行的用户身份 
user = test

#日志输出 
stderr_logfile=/tmp/blog_stderr.log 
stdout_logfile=/tmp/blog_stdout.log 
#把stderr重定向到stdout，默认 false
redirect_stderr = true
#stdout日志文件大小，默认 50MB
stdout_logfile_maxbytes = 20M
#stdout日志文件备份数
stdout_logfile_backups = 20
```

- 例子

```python
[program:test] 
directory=/root 
command=/usr/sbin/tinyproxy -c /etc/tinyproxy/tinyproxy.conf
autostart=true 
autorestart=false 
stderr_logfile=/root/tmp/tinyproxy/test_stderr.log 
stdout_logfile=/root/tmp/tinyproxy/test_stdout.log 
#user = test
```

