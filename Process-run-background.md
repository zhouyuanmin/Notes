---
title: Process-run-background
date: 2020-01-06 10:42:01
tags:
- Centos7
categories:
- Linux
---

#### 0. “&” 

```
一般我们可在结尾加上"&"来将命令同时放入后台运行
但是关掉会话之后，进程就会被杀掉
```

#### 1. nohup

```
nohup ping www.ibm.com &
# nohup 的用途就是让提交的命令忽略 hangup 信号
# 标准输出和标准错误缺省会被重定向到 nohup.out 文件中，也可使用 >filename 2>&1 来重定向文件名
nohup python3 run.py >/dev/null 2>&1 &
```

#### 2. setsid

```
setsid ping www.ibm.com
# 将命令进程放到1号进程下面（就不是子进程了，不再接收hangup信号）
```

#### 3. subshell 的小技巧

```
(ping www.ibm.com &)
# 括号包起来
# 让命令在subshell运行
# 父 ID（PPID）为1，不属于当前终端的子进程，从而也就不会受到当前终端的 HUP 信号的影响了。
```

#### 相关链接

[让进程在后台运行更可靠的几种方法](https://www.ibm.com/developerworks/cn/linux/l-cn-nohup/)