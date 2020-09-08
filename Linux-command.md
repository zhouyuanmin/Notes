---
title: Linux-command
date: 2020-01-29 01:48:56
tags:
- Linux
categories:
- Linux
keywords:
- Port
---

#### port

```python
# 查看占用端口的进程
netstat -tlnp|grep 6379  # t-tcp,l-listen,n-不解析(速度快),p-process
# 一次性的清除占用80端口的程序
lsof -i :80|grep -v "PID"|awk '{print "kill -9",$2}'|sh
# 终止进程
kill 5014
# 强制终止进程
kill -9 5014  # 是pid
```

