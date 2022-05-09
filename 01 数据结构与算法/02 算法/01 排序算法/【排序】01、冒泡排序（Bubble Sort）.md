<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-03-02 14:17:19 -->

[TOC]

---

## 排序原理

冒泡排序（Bubble Sort）是一种交换排序。

- 重复地遍历序列
  - 两两比较相邻记录的关键字
    - 如果正序，则不操作；
    - 如果反序，则交换位置。

> ***💬说明：*** *由于越小（大）的元素会经过交换“浮”到序列的顶端，如同 CO~2~ 气泡浮到顶端一般，故名“冒泡排序”。*



## 时间复杂度

- 定义**关键字比较次数** $C$ 和**记录移动次数为** $M$

  - 当序列为正序时
    $$
    C_{min}=n-1 \Rightarrow O(n)
    \\
    M_{min}=0 \Rightarrow O(1)
    \tag{1.1}
    $$
    
  - 当序列为逆序时
    $$
    C_{max}=\frac{n(n-1)}{2} \Rightarrow O(n^2)
    \\
    M_{max}=\frac{3n(n-1)}{2} \Rightarrow O(n^2)
    \tag{1.2}
    $$
  
- 平均时间复杂度为

$$
O(n^2) \tag{1.3}
$$





## 空间复杂度

$$
O(1) \tag{2}
$$



## 稳定性

稳定



## 动图演示

<div align="center">
<img src="https://www.runoob.com/wp-content/uploads/2019/03/bubbleSort.gif" />
</div>



## 代码实现

### Python

```python
def bubbleSort(arr) -> list:
    '''
    * 冒泡排序
    * 大的往下沉，小的往上冒
    :param arr: 排序前的列表
    :return: 排序后的列表
    '''

    # i 表示第几轮比较（10 个数字需要进行 9 轮比较）
    for i in range(0, len(arr)-1):
        for j in range(len(arr) - 1, i, -1):
            if arr[j] < arr[j-1]:
                # 交换 arr[j-1] 和 arr[j]
                arr[j-1], arr[j] = arr[j], arr[j-1]
    return arr
```



## 代码优化

### Python

```python

def bubbleSort(arr) -> list:
    '''
    * 冒泡排序
    * 大的往下沉，小的往上冒
    :param arr: 排序前的列表
    :return: 排序后的列表
    '''

    # i 表示第几轮比较（10 个数字需要进行 9 轮比较）
    for i in range(0, len(arr)-1):
        # 立个 Flag（是否有序？）
        flag = True
        for j in range(len(arr) - 1, i, -1):
            if arr[j] < arr[j-1]:
                # 交换 arr[j-1] 和 arr[j]
                arr[j-1], arr[j] = arr[j], arr[j-1]
                flag = False
        if flag:
            break
    return arr
```

- 增加序列是否有序的判断，避免在有序的条件下进行无意义的循环

$$
T_{min}(n)=\underbrace{1+1+1+\cdots+1}_{n-1个}=n-1 \Rightarrow O(n)
\\
T_{max}(n)=1+2+3+\cdots+(n-1)=\frac{n(n-1)}{2} \Rightarrow O(n^2)
\tag{3}
$$

