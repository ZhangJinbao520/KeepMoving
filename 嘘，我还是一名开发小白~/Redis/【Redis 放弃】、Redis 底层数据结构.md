<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-01-04 13:33:18 -->

[TOC]

## Redis 对象

Redis 对象是由`RedisObject`组成的，该结构中和保存数据相关的三个属性分别是：

- **type**：对象的类型
- **encoding**：对象的编码
- **lru**：对象最后一次被访问的时间
- **refcount**：引用计数器
- **\*ptr**：指向实际值的指针

```c
// Redis 对象
typedef struct redisObject {

    // 类型
    unsigned type : 4;

    // 编码
    unsigned encoding : 4;

    // 对象最后一次被访问的时间
    unsigned lru : LRU_BITS; /* LRU time (relative to global lru_clock) or
                              * LFU data (least significant 8 bits frequency
                              * and most significant 16 bits access time). */

    // 引用计数器
    int refcount;

    // 指向实际值的指针
    void *ptr;

} robj;
```



## Type

Redis 有 5 种对象类型，如下所示：

- **STRING**
- **LIST**
- **SET**
- **ZSET**
- **HASH**

```c
/* The actual Redis Object */
#define OBJ_STRING 0    /* String object. */
#define OBJ_LIST 1      /* List object. */
#define OBJ_SET 2       /* Set object. */
#define OBJ_ZSET 3      /* Sorted set object. */
#define OBJ_HASH 4      /* Hash object. */
```



## Encoding

Redis 有 12 种数据结构，如下所示：

- **RAW**
- **INT**
- **HT**
- **ZUOMAO**
- **LINKEDLIST**
- **ZIPLIST**
- **INTSET**
- **SKIPLIST**
- **EMBSTR**
- **QUICKLIST**
- **STREAM**
- **LISTPACK**

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

| 编码                    | 说明                        |
| :---------------------- | --------------------------- |
| OBJ_ENCODING_RAW        | 简单动态字符串              |
| OBJ_ENCODING_INT        | long 类型的整数             |
| OBJ_ENCODING_HT         | 字典                        |
| OBJ_ENCODING_ZIPMAP     | 旧的表示方式（已不再使用）  |
| OBJ_ENCODING_LINKEDLIST | 双端链表                    |
| OBJ_ENCODING_ZIPLIST    | 压缩列表                    |
| OBJ_ENCODING_INTSET     | 整数集合                    |
| OBJ_ENCODING_SKIPLIST   | 跳跃表和字典                |
| OBJ_ENCODING_EMBSTR     | EMBSTR 编码的简单动态字符串 |
| OBJ_ENCODING_QUICKLIST  |                             |
| OBJ_ENCODING_STREAM     |                             |
| OBJ_ENCODING_LISTPACK   |                             |



## Type 和 Encoding 关系

| 类型       | 编码                    | 对象                                             |
| ---------- | :---------------------- | ------------------------------------------------ |
| OBJ_STRING | OBJ_ENCODING_RAW        | 使用简单动态字符串实现的字符串对象               |
| OBJ_STRING | OBJ_ENCODING_INT        | 使用整数值实现的字符串对象                       |
| OBJ_HASH   | OBJ_ENCODING_HT         | 使用字典实现的哈希对象                           |
|            | OBJ_ENCODING_ZIPMAP     |                                                  |
| OBJ_LIST   | OBJ_ENCODING_LINKEDLIST | 使用双端链表实现的列表对象                       |
| OBJ_LIST   | OBJ_ENCODING_ZIPLIST    | 使用压缩列表实现的列表对象                       |
| OBJ_SET    | OBJ_ENCODING_INTSET     | 使用整数集合实现的集合对象                       |
|            | OBJ_ENCODING_SKIPLIST   |                                                  |
| OBJ_STRING | OBJ_ENCODING_EMBSTR     | 使用 EMBSTR 编码的简单动态字符串实现的字符串对象 |
|            | OBJ_ENCODING_QUICKLIST  |                                                  |
|            | OBJ_ENCODING_STREAM     |                                                  |
|            | OBJ_ENCODING_LISTPACK   |                                                  |
| OBJ_HASH   | OBJ_ENCODING_ZIPLIST    | 使用压缩列表实现的哈希对象                       |
| OBJ_SET    | OBJ_ENCODING_HT         | 使用字典实现的集合对象                           |
| OBJ_ZSET   | OBJ_ENCODING_ZIPLIST    | 使用压缩列表实现的有序集合对象                   |
| OBJ_ZSET   | OBJ_ENCODING_SKIPLIST   | 使用跳跃表和字典实现的有序集合对象               |
