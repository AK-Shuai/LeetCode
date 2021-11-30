# 快速排序的四种python实现（原文参考）

快速排序算法，简称快排，是最实用的排序算法，没有之一，各大语言标准库的排序函数也基本都是基于快排实现的。

本文用python语言介绍四种不同的快排实现。 

## 一行代码实现的简洁版本

```python
quick_sort = lambda array: array if len(array) <= 1 else quick_sort([item for item in array[1:] if item <= array[0]]) + [array[0]] + quick_sort([item for item in array[1:] if item > array[0]])
```

## 网上常见的快排实现
```python
def quick_sort(array, left, right):
    if left >= right:
        return
    low = left
    high = right
    key = array[low]
    while left < right:
        while left < right and array[right] > key:
            right -= 1
        array[left] = array[right]
        while left < right and array[left] <= key:
            left += 1
        array[right] = array[left]
    array[right] = key
    quick_sort(array, low, left - 1)
    quick_sort(array, left + 1, high)
```

由于快排是原地排序，因此不需要返回array。

array如果是个列表的话，可以通过len(array)求得长度，但是后边递归调用的时候必须使用分片，而分片执行的原列表的复制操作，这样就达不到原地排序的目的了，所以还是要传上边界和下边界的。

## 算法导论中的快排程序

```python
def quick_sort(array, l, r):
    if l < r:
        q = partition(array, l, r)
        quick_sort(array, l, q - 1)
        quick_sort(array, q + 1, r)

def partition(array, l, r):
    x = array[r]
    i = l - 1
    for j in range(l, r):
        if array[j] <= x:
            i += 1
            array[i], array[j] = array[j], array[i]
    array[i + 1], array[r] = array[r], array[i+1]
    return i + 1
```

这个版本跟上个版本的不同在于分片过程不同，只用了一层循环，并且一趟就完成分片，相比之下代码要简洁的多了。

## 用栈实现非递归的快排程序

先说两句题外话，一般意义上的栈有两层含义，一层是后进先出的数据结构栈，一层是指函数的内存栈，归根结底，函数的内存栈的结构就是一个后进先出的栈。汇编代码中，调用一个函数的时候，修改的也是堆栈指针寄存器ESP，该寄存器保存的是函数局部栈的栈顶，另外一个寄存器EBP保存的是栈底。不知道与栈存储空间相对的堆存储空间，其组织结构是否也是一个完全二叉树呢？

高级语言将递归转换为迭代，用的也是栈，需要考虑两个问题:
1. 栈里边保存什么？
2. 迭代结束的条件是什么？

栈里边保存的当然是需要迭代的函数参数，结束条件也是跟需要迭代的参数有关。对于快速排序来说，迭代的参数是数组的上边界low和下边界high，迭代结束的条件是low == high。

```python
def quick_sort(array, l, r):
    if l >= r:
        return
    stack = []
    stack.append(l)
    stack.append(r)
    while stack:
        low = stack.pop(0)
        high = stack.pop(0)
        if high - low <= 0:
            continue
        x = array[high]
        i = low - 1
        for j in range(low, high):
            if array[j] <= x:
                i += 1
                array[i], array[j] = array[j], array[i]
        array[i + 1], array[high] = array[high], array[i + 1]
        stack.extend([low, i, i + 2, high])
```

另外，当数组下标为-1时，C++、Java等语言中会报错，但python中访问的是最后一个元素，所以如果程序写错了，可能其他语言会报错，但python会输出一个错误的结果。 

## 参考
1. <a href="https://cloud.tencent.com/developer/article/1571782" target="_blank">快速排序的四种python实现</a>
