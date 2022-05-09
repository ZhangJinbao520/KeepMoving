<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-03-02 14:17:19 -->

[TOC]

---

## 排序原理

- 未排序的序列
  - 在已排序的序列中查找适当位置并插入



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
    M_{max}=\frac{n(n-1)}{2} \Rightarrow O(n^2)
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
<img src="https://www.runoob.com/wp-content/uploads/2019/03/insertionSort.gif" />
</div>



## 代码实现

### python

```python
def insertionSort(arr):
    '''
    :param arr: 排序前的数组
    :return: 排序后的数组
    '''

    for i in range(1, len(arr)):
        # 当前需要插入的牌
        insertValue = a[i]
        # 当前插入的牌前面有几张牌（索引从 0 开始数）
        index = i - 1
        # 判断牌是否到顶了
        while index >= 0 and arr[index] > insertValue:
            # 把大的移位到后面
            arr[index+1] = arr[index]
            # 前面的牌数
            index -= 1
        # 插牌
        arr[index+1] = insertValue
    return arr
```

