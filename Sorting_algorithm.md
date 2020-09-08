---
title: Sorting_algorithm
date: 2020-02-22 23:08:11
tags:
- Algorithm
categories:
- Algorithm
keywords:
---

### 排序算法

##### 术语

```
稳定：如果a原本在b前面，而a=b，排序之后a仍然在b的前面；
不稳定：如果a原本在b的前面，而a=b，排序之后a可能会出现在b的后面；
内排序：所有排序操作都在内存中完成；
外排序：由于数据太大，因此把数据放在磁盘中，而排序通过磁盘和内存的数据传输才能进行；
时间复杂度：一个算法执行所耗费的时间。
空间复杂度：运行完一个程序所需内存的大小。
```

##### 算法总结

![算法总结.png](https://images2017.cnblogs.com/blog/849589/201710/849589-20171015233043168-1867817869.png)

```
图片名词解释
n: 数据规模
k: “桶”的个数
In-place: 占用常数内存，不占用额外内存
Out-place: 占用额外内存
```

##### 算法分类

![算法分类.png](https://images2017.cnblogs.com/blog/849589/201710/849589-20171015233220637-1055088118.png)

### 算法详解

##### 1. 冒泡 Bubble Sort

```
相邻两两比较、交换
```

```
最佳情况：T(n) = O(n)   最差情况：T(n) = O(n2)   平均情况：T(n) = O(n2)
```

##### 2. 选择排序 Selection Sort

```
在未排list中找到最小，放到排序后的list末尾
```

```
最佳情况：T(n) = O(n2)  最差情况：T(n) = O(n2)  平均情况：T(n) = O(n2)
```

##### 3. 插入排序 Insertion Sort

```
将未排序的list，一个一个插入到已排序的list中
```

```
最佳情况：T(n) = O(n)   最坏情况：T(n) = O(n2)   平均情况：T(n) = O(n2)
```

##### 4. 希尔排序 Shell Sort

```
插入排序的变种：定义增量，以增量为间隔，进行插入排序，逐渐减小增量
```

```
最佳情况：T(n) = O(nlog2 n)  最坏情况：T(n) = O(nlog2 n)  平均情况：T(n) =O(nlog n)
```

##### 5. 归并排序 Merge Sort

```
将list不断分为两个子序列，直到只有1个或者2个元素（递归）
将两个排序好的子序列合并成一个最终的排序序列（返回值）
```

```
最佳情况：T(n) = O(n)  最差情况：T(n) = O(nlogn)  平均情况：T(n) = O(nlogn)
```

```python
def merge_sort(arr):
    # divide to two
    if len(arr) < 2:
        return arr
    mid = int(len(arr)/2)
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    j = 0
    i = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    # add the larger part both left and right
    result += left[i:]
    result += right[j:]
    return result
```

##### 6. 快速排序 Quick Sort

```
一个基准，左边list小于或等于基准，右边list大于list
```

```
最佳情况：T(n) = O(nlogn)   最差情况：T(n) = O(n2)   平均情况：T(n) = O(nlogn)
```

```python
def qucik_sort(alist):
    if len(alist) <= 1:
        return alist
    return qucik_sort([i for i in alist[1:] if i < alist[0]]) + alist[0:1] + qucik_sort([i for i in alist[1:] if i >= alist[0]])
```

```
一行快排
def qs(a): return qs([i for i in a[1:] if i <= a[0]]) + a[0:1] + qs([i for i in a[1:] if i > a[0]]) if len(a) > 1 else a
```

##### 7. 堆排序 Heap Sort

```
https://blog.csdn.net/weixin_40596016/article/details/79711682
```

##### 8. 计数排序 Counting Sort

```
它只能对整数进行排序
```

```
最佳情况：T(n) = O(n+k)  最差情况：T(n) = O(n+k)  平均情况：T(n) = O(n+k)
```

##### 9. 桶排序 Bucket Sort

```
桶排序是计数排序的升级版
```

```
最佳情况：T(n) = O(n+k)   最差情况：T(n) = O(n+k)   平均情况：T(n) = O(n2)
```

##### 10. 基数排序 Radix Sort

```
最佳情况：T(n) = O(n * k)   最差情况：T(n) = O(n * k)   平均情况：T(n) = O(n * k)
```

