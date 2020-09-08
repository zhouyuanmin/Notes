---
title: Scrapy_shell
date: 2020-02-22 02:08:11
tags:
- Scrapy
categories:
- Scrapy
keywords:
- Shell
---

#### shell

```python
# 给scrapy shell 调试加上headers
scrapy shell # 进入shell,但没有url
headers = {'User-Agent': 'User-Agent:Mozilla/5.0 (Windows NT 6.1; rv:2.0.1) Gecko/20100101 Firefox/4.0.1'}
req = scrapy.Request(url='url',headers=headers)
fetch(req) # 如此就等价于scrapy shell url # 添加了headers
```

