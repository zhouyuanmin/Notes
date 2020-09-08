---
title: Interview-2
date: 2020-01-27 22:28:51
tags:
- Interview
- Linux
categories:
- Interview
keywords:
- Linux
---

```python
# 日志以文本可以存储在“/var/log/”目录下后缀名为.log
```

```python
# 查看服务占用的端口
netstat -anp | grep service_name
```

```python
grep 是查找匹配条件的行
find 是搜索匹配条件的文件（找文件）
```

```python
# Linux 重定向命令有哪些？有什么区别?
1. 重定向>   覆盖
2. 重定向>>  追加
```

```python
# 10 个常用的 Linux 命令
pwd 显示工作路径
ls 查看目录中的文件
rm -f file1   # 删文件 -f 不给提示
rmdir dir1    # 删目录
groupadd group_name # 创建一个新用户组
groupdel group_name # 删除一个用户组
tar -cvf archive.tar file1 file2 dir1  # 创建一个非压缩的 tar包
tar -tf archive.tar # 显示一个包中的内容
tar -xvf archive.tar -C /tmp # 解压压缩包到/tmp目录下
# -c 压缩 -x 解压 -v 显示所有过程 -f 压缩包名字
tar -cvfj archive.tar.bz2 dir1  # 创建一个 bzip2 格式的压缩包
tar -xvfj archive.tar.bz2       # 解压一个 bzip2 格式的压缩包
tar -cvfz archive.tar.gz dir1   # 创建一个 gzip 格式的压缩包
tar -xvfz archive.tar.gz        # 解压一个 gzip 格式的压缩包
```

```python
# 关机
reboot  # 重启
shutdown –r now  # 重启，会给其他用户提示
shutdown -h 20:25   #  定时关机
shutdown -h +10  # 十分钟后关机
init 0  # 关机
init 6  # 重启
```

