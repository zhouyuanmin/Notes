---
title: Interview-5
date: 2020-01-28 13:33:29
tags:
- Interview
categories:
- Interview
keywords:
- 本节，不细讲，自己看书研究与学习
---

#### 系统编程

```python
# 进程总结
# 程序运行在操作系统上的一个实例，就称之为进程。
# 进程需要相应的系统资源：内存、时间片、pid
from multiprocessing import Process

proc = Process(target=func, args=(1,), kwargs={'a': 'a'}, name='proc_1')
proc.start()
proc.is_alive()  # 是否还活着
proc.join(timeout=10)  # 等结束，或者等10秒
proc.terminate()  # 强制关闭
proc.name
proc.pid
```

```python
# 进程之间的通信-Queue  # 只用于本机，不能注册到网络上
from multiprocessing import Queue
que = Queue(maxsize=0)  # 可以指定最大容量
que.qsize()  # 返回当前包含的消息数量
que.empty()  # 为空返回True
que.full()   # 满了返回True
que.get(block=True,timeout=None)  # 超时,抛出"Queue.Empty"异常
que.put(item,block=True,timeout=None)  # 超时,抛出"Queue.Full"异常
```

```python
# 进程池-Pool
from multiprocessing import Pool

pool = Pool(3)
pool.apply_async(func=func, args=(), kwds={}, callback=None, error_callback=None)
pool.close()   # 必须关闭
pool.join()
pool.terminate()
# 如果要使用 Pool 创建进程，就需要使用 multiprocessing.Manager()中的 Queue()
# 不能使用multiprocessing.Queue()
from multiprocessing import Manager
q = Manager().Queue()
```

#### 你对多进程，多线程，以及协程的理解，项目是否用？

```python
# 进程：一个运行的程序（代码）就是一个进程，没有运行的代码叫程序，进程是系统资源分配的最小单位，进程拥有自己独立的内存空间，所以进程间数据不共享，开销大。
# 线程： 调度执行的最小单位，也叫执行路径，不能独立存在，依赖进程存在一个进程至少有一个线程，叫主线程，而多个线程共享内存(数据共享，共享全局变量)，从而极大地提高了程序的运行效率。
# 协程：是一种用户态的轻量级线程，协程的调度完全由用户控制。协程拥有自己的寄存器上下文和栈。 协程调度切换时，将寄存器上下文和栈保存到其他地方，在切回来的时候，恢复先前保存的寄存器上下文和栈，直接操作栈则基本没有内核切换的开销，可以不加锁的访问全局变量，所以上下文的切换非常快。
```

#### 什么是多线程竞争？

```python
# 线程是非独立的，同一个进程里线程是数据共享的，当各个线程访问数据资源时会出现竞争状态即：数据几乎同步会被多个线程占用，造成数据混乱 ，即所谓的线程不安全
```

```python
# 那么怎么解决多线程竞争问题？-- 锁。
# 锁的好处：确保了某段关键代码(共享数据资源)只能由一个线程从头到尾完整地执行能解决多线程资源竞争下的原子操作问题。
# 锁的坏处：阻止了多线程并发执行，包含锁的某段代码实际上只能以单线程模式执行，效率就大大地下降了
# 锁的致命问题：死锁。
```

#### 什么是死锁？

```python
# 若干子线程在系统资源竞争时，都在等待对方对某部分资源解除占用状态，结果是谁也不愿先解锁，互相干等着，程序无法执行下去，这就是死锁。
# GIL锁
# 全局解释器锁（只在 cpython 里才有）
# 作用：限制多线程同时执行，保证同一时间只有一个线程执行，所以 cpython 里的多线程其实是伪多线程!
# 所以 Python 里常常使用协程技术来代替多线程，协程是一种更轻量级的线程
# 进程和线程的切换时由系统决定，而协程由我们程序员自己决定，而模块 gevent 下切换是遇到了耗时操作才会切换。
# 三者的关系：进程里有线程，线程里有协程。
```

