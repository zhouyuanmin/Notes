---
title: Shell
date: 2020-03-20 20:10:58
tags:
- Shell
categories:
- Shell
keywords:
---

#### Shell脚本格式

```shell
#!/bin/bash   开头指定解释器
```

##### 语法

```
# 输出
echo 'Hello World...'
source 配置文件  # 让修改后的配置信息立即生效
# chmod 744 myshell.sh  # 授权
```

##### 变量

```
# 系统变量
env命令 可以查看系统全局变量
printenv命令 查看指定环境变量的值 等价于$USER
例子 $HOME $PWD $SHELL $USER
# 用户自定义变量
声明是 echo $A # 可以直接定义,不声明
A=100  # 定义  如果变量值有空格时，必须加双引号。
使用是 B=$A  # 定义静态变量：readonly A=90 但是不能unset  
unset a  # 删除变量 在unset引用变量名时，不要加$。
# set 显示当前shell中所有变量
# 变量一般为大写，等号左右不能有空格
```

```
创建全局变量的方法是先创建一个局部变量,然后导出到全局环境中
export A
在子shell中修改全局变量并不会影响到父shell中该变量的值。
```

##### 将命令结果赋值给变量

```
A=$(ls -a)  等价于 A=`ls -a`  # 反引号 
```

##### 注释

```shell
# 单行注释
# 多行注释如下
:<<!
语句
!
```

##### 位置参数变量

```
语法有$n和$*和$@和$#和${10}
$$ 当前进程PID
$! 后台运行的最后一个进程的PID
$? 最后一次执行的命令的返回状态,0正确，非零执行不正确
```

##### 运算符

```
((运算式))和$[运算式]  # 推荐使用$[运算式]  # 没有expr
# expr m + n  # 可以 + - \* / % 加 减 乘 除 取余
```

##### 条件判断

```shell
# 基本语法和格式
[ condition ]（注意 condition 前后要有空格）
非空返回 true，可使用$?验证（结果为：0 为 true，>1 为 false）
# 常用判断条件（左右两边有空格）
= 字符串比较
-lt 小于
-le 小于等于
-eq 等于
-gt 大于
-ge 大于等于
-ne 不等于
# 按照文件权限进行判断
-r 有读的权限 [ -r 文件 ]
-w 有写的权限
-x 有执行的权限
# 按照文件类型进行判断  # 例子 [ -e /root/a.txt ]
-f 文件存在并且是一个常规的文件
-e 文件存在
-d 文件存在并是一个目录
```

```shell
# if 格式
#!/bin/bash
if [ "str" = "s1tr" ]
then
    echo "str equal"
elif [ 100 = 101 ]
then
    echo "100 equal"
elif [ "str1" = "str1" ]
then
    echo "str1 equal"
	if [ 123 = 123 ]
    then
        echo "123 equal"
    else
        echo "123 not equal"
	fi
fi
```

```shell
# case语句
case $变量名 in 
    "值1")
        语句
        ;;
    "值2")
        语句
        ;;
    *)
        语句
        ;;
esac
```

```shell
# for 语句
# 实例1
for i in 1 2 3 4  # 1 2 3 4 可以替换为 "$*"和"$@"
do
   echo "$i"
done
# 实例2
for((i=1;i<=100;i++))
do
    echo "$i"
done
```

```shell
# while 语句
i=1
while [ $i -le 10 ]
do 
    echo "num=$i"
    i=$[$i+1]  # 加一
    let i=$i+1 # 加一   # let ：用来执行算数运算和数值表达式测试
    let i++    # 加一   # let 命令的替代表示形式是 ((算术表达式))
done
```

##### 控制台输入

```shell
read -p "请输入一个数num1=" -t 10 NUM1  # -p 为提示符 -t 是等待时间
```

##### 函数

```shell
# 系统函数
basename [string] [suffix] # 返回文件名
suffix 为后缀，如果 suffix 被指定了，basename 会将 string 中的 suffix 去掉。
# 系统函数
dirname 文件绝对路径  # 返回目录
返回完整路径最后'/'的前面的部分，常用于返回路径部分
```

```shell
# 自定义函数
#!/bin/bash
function get_sum(){
    local sum=0  #局部变量
    sum=$[$sum+$1+$2]
    echo $sum
    return $?
}
m=100
n=200
total=$(get_sum $m $n)
echo "The sum is $total"
```

##### 附加

```shell
vim命令
set tabstop=4
set nu
set nonu
G
gg
u # 撤销
shift+g
```

