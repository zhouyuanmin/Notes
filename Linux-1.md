---
title: Linux-1
date: 2020-03-18 01:16:17
tags:
- Linux
categories:
- Linux
keywords:
---

#### Linux复习笔记

##### 用户管理

```
# 1.添加用户
useradd xm
useradd -d /home/xm xm  # 指定家目录
useradd -g gxm xm  # 指定用户组gxm
# 2.密码
passwd xm
# 3.删除用户
userdel xm
userdel -r xm  # 删除家目录
# 4.查询用户信息
id xm
# 5.切换用户
su xm
exit  # 退回原来的用户
# 6.修改用户的组
usermod -g gxm xm
# 7.修改用户家目录
usermod -d /home/xm xm
```

##### 用户组管理

```
# 1.添加用户组
groupadd xm
# 2.删除用户组
groupdel xm
```

##### 用户相关文件

```
# 用户的配置文件，记录用户的各种信息（用户名，用户id，组id，家目录，shell）
/etc/passwd
# 密码的配置文件（登录名:加密口令:最后修改时间:最小间隔:最大间隔:警告时间:不活动时间:失效时间:标志）
/etc/shadow
# 组的配置文件（组名，组id）
/etc/group
```

##### 文件权限管理

```
chown xm a.txt  # 修改所属用户 
chgrp gxm a.txt  # 修改所属组
chown xm:gxm a.txt  # 同时修改（特殊用法）
-R  递归生效
# 修改文件权限 u g o a 可以 +- rwx
chmod o-x a.txt
chmod 421 a.txt # r-- -w- --x
```

##### 任务调度

```shell
# /etc/crontab  # 服务名为 crond  
# systemctl restart crond
crontab  
-e 编辑  # 格式*/1 8,12 * * 0-7 ll /root >> /root/to.log  # *和,和-和*/n
        # 格式 * * * * * /home/mytask1.sh # 直接跟shell脚本 # 要注意执行权限
-l 查询
-r 删除当前用户所有的crontab任务
```

