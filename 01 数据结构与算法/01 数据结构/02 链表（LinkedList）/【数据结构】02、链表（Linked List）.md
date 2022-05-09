<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-04-25 10:53:45 -->

[TOC]

---

## 什么是链表？

链表（Linked List）是一种**链式存储**的线性表，它通过“**指针**”将一组零散的内存地址，在**逻辑**上虚拟成连续的内存空间；其主要特性如下：

- <font color="red">**内存地址不一定连续**</font>
- <font color="red">**指针**</font>

<div align="center">
    <img src="https://img2018.cnblogs.com/blog/1468033/201905/1468033-20190528214004111-1104525480.png" />
</div>



## 概念定义

- **结点**

  - **数据**

  - **前驱指针（prev）**

    记录上一个结点地址的指针。

  - **后继指针（next）**

    记录下一个结点地址的指针。

- **头结点**

  记录链表的**基地址**。

- **尾结点**

  记录链表的**尾地址**。



## 单链表（Single LinkedList）

<div align="center">
    <img src="https://img2018.cnblogs.com/blog/1468033/201905/1468033-20190528214524891-532231990.png" />
</div>

### 增（插入）

- **复杂度**
  - 最好复杂度：$O(1)$
  
    > ***💬说明：*** *链表开头。*

  - 最坏复杂度：$O(n)$
  
    > ***💬说明：*** *链表末尾。*
  
  - 平均复杂度：$O(n)$
  
- **算法逻辑**（定义链表为 $a$，链表长度为 $n$）

  - 查询 $a_{k-1}$
- 插入 $a_k$
  - $a_{k-1}.next->a_{k}$
- $a_{k}.next->a_{k+1}$

<div align="center">
    <img src="https://img2018.cnblogs.com/blog/1468033/201905/1468033-20190528215024519-1999572279.png" />
</div>



## 双链表

<div align="center">
    <img src="https://img2018.cnblogs.com/blog/1468033/201905/1468033-20190528220633117-1035612130.png" />
</div>



## 循环链表

<div align="center">
    <img src="https://img2018.cnblogs.com/blog/1468033/201905/1468033-20190528215849268-1817142708.png" />
</div>
