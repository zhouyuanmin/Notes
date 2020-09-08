# Python常用内置库

### 0.内置函数

- chr()   转换一个[0, 255]之间的整数为对应的ASCII字符
- ord()   将一个ASCII字符转换为对应整数

### 1.copy

- copy.deepcopy(a)
- copy.copy(a)

### 2.random

- random.shuffle(list)  洗牌
- random.randint(a,b)  随机整数[a,b]
- random.random()  随机(0,1)
- random.choice(seq)
- random.randrange(0, 101, 2)   包前不包后

### 3.os

- 负责与操作系统交互
- os.remove()
- os.rename(src, dst)  重命名
- os.mkdir()
- os.remkdir()  删除目录
- os.getcwd()
- os.chdir()  改变当前脚本的工作路径，相当于shell下的cd

### 4.sys

- 负责与Python解释器交互
- sys.exit(0)
- sys.path 解释器的环境变量是list格式

### 5.time

- time.time()  时间戳数字
- time.localtime()   返回struct_time对象
- time.asctime()  格式化输出
- time.strftime("%Y-%m-%d %H:%M:%S")   格式化输出
- time.strptime("2016/05/22","%Y/%m/%d")    返回struct_time对象

### 6.datetime

- a = datetime.datetime.now()
- a.strftime("%Y-%m-%d %H:%M:%S")   格式化输出
- a.utctimetuple()   # 返回struct_time对象，与time.localtime()对象类型相同，值也相同
- datetime.timedelta(day=3, hours=12, minutes=30, seconds=30)