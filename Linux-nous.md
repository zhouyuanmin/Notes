---
title: Linux-nous
date: 2020-01-08 12:57:28
tags:
- Linux
categories:
- Linux
---

#### 问题

```python
You have new mail in /var/spool/mail/root
# 这个提示是LINUX会定时查看LINUX各种状态做汇总，每经过一段时间会把汇总的信息发送的root的邮箱里，以供有需之时查看
# 一般这种情况mail的内容就只是一些正常的系统信息或者是比较重要的错误报告。
```

#### 解决方案

- 关闭提示

```
echo "unset MAILCHECK">> /etc/profile
source /etc/profile
```

- 查看

```
ls -lth /var/spool/mail/
```

- 清空

```
cat /dev/null > /var/spool/mail/root
```

