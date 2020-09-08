---
title: Beethoven-2
date: 2020-01-18 20:26:30
tags:
- Beethoven
categories:
- Beethoven
keywords:
- Beethoven
---

#### socket

- TCP

```python
# TCP客户端
import socket
s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(('www.baidu.com',80))
s.send(bytes)  # 发送
s.recv(1024)  # 接收bytes,没有数据了，则为空
s.close()
# TCP服务端
s.bind(('127.0.0.1', 80))  # 对外服务绑定0.0.0.0
s.listen(5)  # 等待连接的最大数量
while True:
    # 接受一个新连接:
    sock, addr = s.accept()  # sock是socket对象,addr是客户端ip地址
    # 创建新线程来处理TCP连接:
    t = threading.Thread(target=tcplink, args=(sock, addr))
    t.start()
def tcplink(sock, addr):
    ...
    sock.close()    
```

- UDP

```python
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.bind(('127.0.0.1', 80))
data, addr = s.recvfrom(1024)  # 接收
s.sendto(data, ('127.0.0.1', 80))  # 发送
s.close()
```

#### SMTP发送邮件

- email构建邮件，smtplib发送邮件

```python
from email.header import Header
from email.mime.text import MIMEText
# 邮件一般是由标题，发信人，收件人，邮件内容，附件等构成
msg = MIMEText('hello,send by python...', 'plain', 'utf-8')  # 内容
msg['From'] = Header('Jason')  # 发件人
msg['To'] = Header('Administrators')  # 收件人
msg['Subject'] = Header('来自SMTP的问候', 'utf-8')  # 标题

import smtplib
server = smtplib.SMTP("smtp.qq.com", 25)
# server.set_debuglevel(1)   # 打印详细
server.starttls()  # 加密
server.login("1837722596@qq.com", "gphfapcvqmjubeje")  # 授权码
server.sendmail("1837722596@qq.com", ["17859717522@163.com", "923810495@qq.com"], msg.as_string())
server.quit()
```

#### POP3收取邮件

- email解析邮件，poplib下载邮件

```python
# 可以不掌握
import poplib
server = poplib.POP3("pop.qq.com")
server.user("1837722596@qq.com")
server.pass_("gphfapcvqmjubeje")
server.stat()   # stat()返回邮件数量和占用空间
```

#### 使用SQLite

```python
# SQLite是一种嵌入式数据库，它的数据库就是一个文件。
# SQLite本身是C写的,而且体积很小,轻量级、可嵌入
import sqlite3
conn = sqlite3.connect('test.db')
cursor = conn.cursor()
cursor.execute('sql')
# cursor对象存储了执行sql语句的结果
# values = cursor.fetchall()  # 获取查询结果集,是list类型,里面是tuple对应一行记录.
# cursor.rowcount  # 获取受影响的行数 
cursor.close()
conn.commit()  # 提交事务，非常重要
conn.close()
# 参数问题  使用'?'占位符
cursor.execute('select * from user where name=? and pwd=?', ('abc', 'password'))
```

#### 使用MySQL

```python
# MySQL常用引擎是InnoDB
mysql -u root -p   # 登陆
show variables like '%char%';   # 检查编码格式,推荐在配置文件中设置为utf8mb4
```

```python
from mysql import connector
conn = connector.connect(user='root',password='pass',database='test')
cursor = conn.cursor()
cursor.execute('sql')
# 其他操作与SQLite使用相同
# (不同点):MySQL的SQL占位符是%s
```

#### 使用SQLAlchemy

```python
# SQLAlchemy是python中最著名的ORM（Object Relationship Mapping）框架
# ORM框架的作用就是把数据库表的一行记录与一个对象互相做自动转换
# pip install sqlalchemy
```

[重新学习SQLAIchemy](https://www.liaoxuefeng.com/wiki/1016959663602400/1017803857459008)

#### 前端

```html
<html>
<head>
  <title>Hello</title>
  <style>
    h1 {
      color: #333333;
      font-size: 48px;
      text-shadow: 3px 3px 3px #666666;
    }
  </style>
  <script>
    function change() {
      document.getElementsByTagName('h1')[0].style.color = '#ff0000';
    }
  </script>
</head>
<body>
  <h1 onclick="change()">Hello, world!</h1>
</body>
</html>
```

#### WSGI接口

- Web Server Gateway Interface

```python
def application(environ, start_response):
    start_response('200 OK', [('Content-Type', 'text/html')])  # headers
    return [b'<h1>Hello, web!</h1>']   # body
# environ：一个包含所有HTTP请求信息的dict对象
# start_response：一个发送HTTP响应的函数，headers
# application()函数必须由WSGI服务器来调用
# environ['PATH_INFO'][1:]  # [1:]是为了去掉/
```

```python
# 认识原理,此代码不具有实用价值  # 处理不同HTTP方法
def application(environ, start_response):
    method = environ['REQUEST_METHOD']
    path = environ['PATH_INFO']
    if method=='GET' and path=='/':
        return handle_home(environ, start_response)
    if method=='POST' and path='/signin':
        return handle_signin(environ, start_response)
    ...
```

#### flask

```python
from flask import Flask
from flask import request
app = Flask(__name__)  # 创建app
@app.route('/',methed=['GET','POST'])
def home():
    return '<h1>Home</h1>'
@app.route('/signin',methed=['GET'])
def signin_form():
    return '''<form action="/signin" method="post">
              <p><input name="username"></p>
              <p><input name="password" type="password"></p>
              <p><button type="submit">Sign In</button></p>
              </form>'''
@app.route('/signin', methods=['POST'])
def signin():
    if request.form['username']=='admin' and request.form['password']=='password':
        return '<h3>Hello, admin!</h3>'
    return '<h3>Bad username or password.</h3>'

if __name__ == '__main__':
    app.run()
```

