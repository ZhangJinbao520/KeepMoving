<!-- @title: 【Redis】Redis 底层数据结构 -->
<!-- @date: 2022-01-04 13:33:18 -->
<!-- @author: Zhang Jinbao -->
<!-- Table of Content -->

[TOC]

## Redis 对象

Redis 对象是由`RedisObject`组成的，该结构中和保存数据相关的三个属性分别是：

- **type**（类型）
- **encoding**（编码）
- ***ptr**（值指针）

```c
// Redis 对象
typedef struct redisObject {
    unsigned type:4;
    unsigned encoding:4;
    unsigned lru:LRU_BITS; /* LRU time (relative to global lru_clock) or
                            * LFU data (least significant 8 bits frequency
                            * and most significant 16 bits access time). */
    int refcount;
    void *ptr;
} robj;
```



## Type

Redis 有 5 种数据类型，如下所示：

- **string**
- **list**
- **set**
- **zset**
- **hash**

```c
/* The actual Redis Object */
#define OBJ_STRING 0    /* String object. */
#define OBJ_LIST 1      /* List object. */
#define OBJ_SET 2       /* Set object. */
#define OBJ_ZSET 3      /* Sorted set object. */
#define OBJ_HASH 4      /* Hash object. */
```



## Encoding

Redis 有 12 种数据类型，如下所示：

```c
/* Objects encoding. Some kind of objects like Strings and Hashes can be
 * internally represented in multiple ways. The 'encoding' field of the object
 * is set to one of this fields for this object. */
#define OBJ_ENCODING_RAW 0     /* Raw representation */
#define OBJ_ENCODING_INT 1     /* Encoded as integer */
#define OBJ_ENCODING_HT 2      /* Encoded as hash table */
#define OBJ_ENCODING_ZIPMAP 3  /* Encoded as zipmap */
#define OBJ_ENCODING_LINKEDLIST 4 /* No longer used: old list encoding. */
#define OBJ_ENCODING_ZIPLIST 5 /* Encoded as ziplist */
#define OBJ_ENCODING_INTSET 6  /* Encoded as intset */
#define OBJ_ENCODING_SKIPLIST 7  /* Encoded as skiplist */
#define OBJ_ENCODING_EMBSTR 8  /* Embedded sds string encoding */
#define OBJ_ENCODING_QUICKLIST 9 /* Encoded as linked list of listpacks */
#define OBJ_ENCODING_STREAM 10 /* Encoded as a radix tree of listpacks */
#define OBJ_ENCODING_LISTPACK 11 /* Encoded as a listpack */
```



## Type 和 Encoding 关系

| 编码类型                | 编码所对应的底层数据结构    | 数据类型 |
| :---------------------- | --------------------------- | -------- |
| OBJ_ENCODING_INT        | long 类型的整数             | string   |
| OBJ_ENCODING_EMBSTR     | embstr 编码的简单动态字符串 | string   |
| OBJ_ENCODING_RAW        | 简单动态字符串              | string   |
| OBJ_ENCODING_HT         | 字典                        | hash     |
| OBJ_ENCODING_ZIPMAP     |                             |          |
| OBJ_ENCODING_LINKEDLIST | 双向链表                    | list     |
| OBJ_ENCODING_ZIPLIST    | 压缩列表                    |          |
| OBJ_ENCODING_INTSET     | 整数集合                    |          |
| OBJ_ENCODING_SKIPLIST   | 跳跃表和字典                |          |
| OBJ_ENCODING_QUICKLIST  |                             |          |
| OBJ_ENCODING_STREAM     |                             |          |
| OBJ_ENCODING_LISTPACK   |                             |          |
