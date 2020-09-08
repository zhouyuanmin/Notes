---
title: Scrapy_1
date: 2020-02-16 23:40:32
tags:
- Scrapy
categories:
- Scrapy
keywords:
- Scrapy
---

```
命令加上参数 --nolog 可以去掉log日志输出
```

#### 异常处理

```python
from scrapy.downloadermiddlewares.retry import RetryMiddleware # 参考这个写即可
# 设置最大等待时间、失败重试次数
DOWNLOAD_TIMEOUT = 10
RETRY_ENABLED = True  # 失败重试
RETRY_TIMES = 5
```

#### scrapy复习笔记

```python
allowed_domains = [] # 与OffsiteMiddleware中间件挂钩
```

```python
scrapy.FormRequest() # post请求
```

```python
from scrapy.downloadermiddlewares.retry import RetryMiddleware 
# 异常处理，必须看源码，必须对异常进行处理
```

##### 选择器

```
get()和getall()
get(default='not-found') #设置默认值
.attrib['src']  # 获取属性值，它返回第一个匹配元素的属性
scrapy css特有的::text和::attr(name)
```

```
>>> response.css('base').attrib   # 变成dict了
{'href': 'http://example.com/'}
>>> response.css('base').attrib['href']
'http://example.com/' 
```

```
# 例子
>>> response.xpath('//base/@href').get()
'http://example.com/'

>>> response.css('base::attr(href)').get()
'http://example.com/'

>>> response.css('base').attrib['href']
'http://example.com/'

>>> response.xpath('//a[contains(@href, "image")]/@href').getall()
['image1.html',
 'image2.html',
 'image3.html',
 'image4.html',
 'image5.html']

>>> response.css('a[href*=image]::attr(href)').getall()
['image1.html',
 'image2.html',
 'image3.html',
 'image4.html',
 'image5.html']

>>> response.xpath('//a[contains(@href, "image")]/img/@src').getall()
['image1_thumb.jpg',
 'image2_thumb.jpg',
 'image3_thumb.jpg',
 'image4_thumb.jpg',
 'image5_thumb.jpg']

>>> response.css('a[href*=image] img::attr(src)').getall()
['image1_thumb.jpg',
 'image2_thumb.jpg',
 'image3_thumb.jpg',
 'image4_thumb.jpg',
 'image5_thumb.jpg']
```

```
>>> response.xpath('//span/text()').get()
'good'
>>> response.css('span::text').get()
'good'
```

```
Selector类可以用文本直接构造，用于xpath解析
>>> from scrapy.selector import Selector
>>> body = '<html><body><span>good</span></body></html>'
>>> Selector(text=body).xpath('//span/text()').get()
'good'
```

```
 response.css('.shout').xpath('./time/@datetime').getall()  # xpath的'.'点号必须加上
```

##### scrapy shell

```python
fetch(url[, redirect=True])   #  Fetch URL and update local objects
fetch(req)                    #  Fetch a scrapy.Request and update local objects
shelp()           # Shell help (print this help)  很重要，常用，类似于help
view(response)    # View response in a browser
```

```python
# scrapy.shell.inspect_response的用法如下：便于运行时，检查
from scrapy.shell import inspect_response
inspect_response(response, self)
```

##### 请求

```
FormRequest.from_response()
```