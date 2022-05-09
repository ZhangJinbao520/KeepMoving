<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-03-02 14:17:19 -->

[TOC]

---

## 排序原理

- 重复地遍历序列
  - 从 n 个元素中找到最小的元素
    - 如果元素索引=0，则不操作；
    - 如果元素索引!=0，则交换位置。

  - 从 n-1个元素中找到最小的元素
    - 如果元素索引=1，则不操作；
    - 如果元素索引!=1，则交换位置。

  - …
  - 从 i 个元素中找到最小的元素
    - 如果元素索引=n-i，则不操作；
    - 如果元素索引!=n-i，则交换位置。

  - …
  - 从 1 个元素中找到最小的元素
    - 如果元素索引=n-1，则不操作；
    - 如果元素索引!=n-1，则交换位置。




## 时间复杂度

- 定义**关键字比较次数** $C$ 和**记录移动次数为** $M$

  - 当序列为正序时
    $$
    C_{min}=\frac{n(n-1)}{2} \Rightarrow O(n^2)
    \\
    M_{min}=0 \Rightarrow O(1)
    \tag{1.1}
    $$
    
  - 当序列为逆序时
    $$
    C_{max}=\frac{n(n-1)}{2} \Rightarrow O(n^2)
    \\
    M_{max}=n-1 \Rightarrow O(n)
    \tag{1.2}
    $$
    
  
- 平均时间复杂度为

$$
O(n^2) \tag{1.3}
$$

> ***💬说明：*** *无论输入数据是什么，选择排序的时间复杂度都为 $O(n^2)$。*



## 空间复杂度

$$
O(1) \tag{2}
$$



## 稳定性

不稳定



## 动图演示

<div align="center">
<img src="https://www.runoob.com/wp-content/uploads/2019/03/selectionSort.gif" />
</div>



## 代码实现

### python

```python
def selectionSort(arr):
    '''
    :param arr: 排序前的列表
    :return: 排序后的列表
    '''

    for i in range(len(arr) - 1):
        # 记录最小数的索引
        minIndex = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[minIndex]:
                minIndex = j
        # i 不是最小数时，将 i 和最小数进行交换
        if i != minIndex:
            arr[i], arr[minIndex] = arr[minIndex], arr[i]
    return arr
```
