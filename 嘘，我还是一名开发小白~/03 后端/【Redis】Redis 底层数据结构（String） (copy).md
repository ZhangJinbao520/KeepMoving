<!-- @title: 【Redis】Redis 底层数据结构 -->
<!-- @date: 2022-01-04 13:33:18 -->
<!-- @author: Zhang Jinbao -->
<!-- Table of Content -->

[TOC]

## String 简介

string 对象的编码类型可以是：

- **int**

- **embstr**

  > 💬**说明**：embstr 是 Redis 用于专门保存字符串的优化编码方式。

- **raw（SDS）**

  > 💬**说明**：在 Redis 数据库中，包含字符串值的键值对底层实现都是基于 SDS 实现的。



## String 何时使用何种编码类型？

具体规则如下：

- 判断字符串是否都为数字？
  - 是，则判断数字是否 ≤2^64 - 1？
    - 是，则采用`int`;
    - 否，则判断字符串长度是否 ≤32 字节？
      - 是，则采用`embstr`；
      - 否，则采用`raw`。
  - 否，则判断字符串长度是否 ≤32 字节？
    - 是，则采用`embstr`；
    - 否，则采用`raw`。

> 💬**说明**：测试版本为 Redis 6.2.6。



## SDS（Simple Dynamic String）

### 数据结构

其数据结构定义如下：

```c
// 定义 SDS
struct sdshdr{
    // 记录 buf 数组已使用的字节长度
    int len;
    // 记录 buf 数组中未使用的字节长度
    int free;
    // 字节数组，用于保存字符串
    char buf[];
};
```

### 特性

- **获取字符串长度的复杂度为 O(1)**

  获取 SDS 字符串长度只需读取 len 属性即可，复杂度为 O(1)；对于 C 语言而言，获取字符串长度需通过遍历计数实现，复杂度为 O(n)。

- **可以杜绝缓冲区溢出**

  - 内存空间是否大于等于 `len`？
    - 如果是，进行修改操作；
    - 如果不是，进行空间扩容，再进行修改操作。

  > 💬**说明**：在 C 语言中，当使用 `strcat` 函数拼接两个字符串时，一旦没有分配足够长度的内存空间，就会导致**缓冲区溢出**。

- **减少修改字符串的内存重新分配次数**

- **二进制安全**

- **兼容部分C字符串函数**

| SDS 字符串                                    | C 字符串                                      |
| --------------------------------------------- | --------------------------------------------- |
| 获取字符串长度的复杂度为 O(1)                 | 获取字符串长度的复杂度为 O(n)                 |
| API 安全                                      | API 不安全                                    |
| 不会造成缓冲区溢出                            | 可能会造成缓冲区溢出                          |
| 修改字符串长度 N 次需执行的内存重分配次数：≤N | 修改字符串长度 N 次需执行的内存重分配次数：=N |
| 可以保存文本数据、或二进制数据                | 只能保存文本数据                              |
| 可以使用一部分<string.h>库函数                | 可以使用所有<string.h>库函数                  |

### 举个栗子🌰

<div align="center">
<img src="https://img-blog.csdnimg.cn/20210227000909729.png" name="SDS 示例"/>
</div>


## LinkList

### 数据结构

其数据结构定义如下：

```c
// 链表节点
typedef struct listNode{
    // 前置节点
    struct listNode *prev;
    // 后置节点
    struct listNode *next;
    // 节点值
    void *value;
} listNode；

// 定义链表
typedef struct list{
    // 表头节点
    listNode *head;
    // 表尾节点
    listNode *tail;
    // 节点值复制函数
    void *(*dup)(void *ptr);
    // 节点值释放函数
    void (*free)(void *ptr);
    // 节点值对比函数
    int (*match)(void *ptr, void *key);
  	// 链表所包含的节点数量
    unsigned long len;
} list;
```

### 特性

- **双端**

  链表具有前置几点和后置节点的引用。

- **无环**

  表头节点的 `prev` 指针和表尾节点的 `next` 指针都只想 **<font color="red">NULL</font>**。

- **长度计数器**

  获取长度的复杂度为 O(1)。

- **多态**

  链表节点使用 `void *value;`保存节点值，可以保存不同类型的值。

### 举个栗子🌰
