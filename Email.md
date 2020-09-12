---
title: Email
date: 2020-03-02 03:58:14
tags:
- Python
categories:
- Python
keywords:
---

#### 发送邮件，带附件

```python
import os
import smtplib
from email import encoders
from email.header import Header
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase


def send_email():
    # 邮件一般是由标题，发信人，收件人，邮件内容，附件等构成
    msg = MIMEMultipart()
    msg['From'] = Header('Worker<1837@qq.com>')  # 发件人
    msg['To'] = Header('Administrators<17859@163.com>')  # 收件人
    msg['Subject'] = Header('Work in 2020.', 'utf-8').encode()  # 标题
    msg.attach(MIMEText('hello, work completed.', 'plain', 'utf-8'))  # 内容

    zip_path = os.path.join(os.path.abspath('.'), 'test.zip')
    with open(zip_path, 'rb') as f:
        mime = MIMEBase('zip', 'zip', filename=zip_path)
        # 加上必要的头信息:
        mime.add_header('Content-Disposition', 'attachment', filename=('utf8', '', 'test1.zip'))
        mime.add_header('Content-ID', '<0>')
        mime.add_header('X-Attachment-Id', '0')
        # 把附件的内容读进来:
        mime.set_payload(f.read())
    encoders.encode_base64(mime)
    msg.attach(mime)

    server = smtplib.SMTP("smtp.qq.com", 25)
    server.starttls()  # 加密
    server.login("196@qq.com", "gphf")  # 授权码
    server.sendmail("186@qq.com", ["17@163.com", ], msg.as_string())
    server.quit()


if __name__ == '__main__':
    send_email()
```

