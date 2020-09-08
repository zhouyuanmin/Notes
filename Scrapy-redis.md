---
title: Scrapy-redis
date: 2020-03-17 04:37:23
tags:
- Scrapy-redis
categories:
- Scrapy-redis
keywords:
- Scrapy-redis
---

#### Scrapy-redis

##### setting

```python
# 启用调度redis中的存储请求队列
SCHEDULER = "scrapy_redis.scheduler.Scheduler"
# 确保所有蜘蛛通过redis共享同一个过滤器。
DUPEFILTER_CLASS = "scrapy_redis.dupefilter.RFPDupeFilter"
# 不清理redis队列，允许暂停/恢复爬网。
SCHEDULER_PERSIST = True
# 使用优先级队列调度请求。（默认）
SCHEDULER_QUEUE_CLASS = 'scrapy_redis.queue.PriorityQueue'
# 备用队列。
SCHEDULER_QUEUE_CLASS = 'scrapy_redis.queue.FifoQueue'
SCHEDULER_QUEUE_CLASS = 'scrapy_redis.queue.LifoQueue'
# 防止蜘蛛在分布式爬网时关闭的最大空闲时间。这仅在队列类为SpiderQueue或SpiderStack时有效，并且在蜘蛛第一次启动时也可能会阻止这么长的时间（因为队列为空）。
SCHEDULER_IDLE_BEFORE_CLOSE = 10
# 将爬取的item存储在redis数据库中
ITEM_PIPELINES = {
    'scrapy_redis.pipelines.RedisPipeline': 300
}
# 存储item的redis的key
REDIS_ITEMS_KEY = '%(spider)s:items'
# 默认情况下，item的序列化程序是ScrapyJSONEncoder。
REDIS_ITEMS_SERIALIZER = 'json.dumps'
# 连接Redis时，使用的主机和端口（可选）。
REDIS_HOST = 'localhost'
REDIS_PORT = 6379
# 指定用于连接Redis的完整URL（可选）。
# 如果设置，它将优先于REDIS_HOST和REDIS_PORT设置。
REDIS_URL = 'redis://user:pass@hostname:9001'
# 自定义Redis客户端参数（即：套接字超时等）
REDIS_PARAMS  = {}
# 是否对初始urls去重，默认False，为不去重
REDIS_START_URLS_AS_SET = False
# 获取起始URL默认的redis key。
REDIS_START_URLS_KEY = '%(name)s:start_urls'
# 使用utf-8以外的其他编码对redis进行编码，默认是utf-8
# REDIS_ENCODING = 'latin1'
```

##### spider编写

```python
class MySpider(RedisSpider):
    name = 'myspider'

    def parse(self, response):
        # do stuff
        pass
```

##### 启动spider

```python
# 1. run the spider:
scrapy runspider myspider.py
# 2. push urls to redis:
redis-cli lpush myspider:start_urls http://google.com
# 两者先后顺序不重要，因为 SCHEDULER_IDLE_BEFORE_CLOSE = 10 会等待
```

