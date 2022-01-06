<!-- @title: 【Redis 入门】03、Redis 五大数据类型 -->
<!-- @date: 2021-12-27 19:43:58 -->
<!-- @author: Zhang Jinbao -->

[TOC]

## Redis 数据类型

Redis 可提供五种数据类型：<font color="purple">string、list、set、zset、hash</font>。

| 数据类型         | 特性                                                      | 适用场景                 |
| ---------------- | --------------------------------------------------------- | ------------------------ |
| string（字符串） | 可以包含任意数据                                          | N/A                      |
| list（双向链表） | 增删快                                                    | 时间线，消息队列         |
| set（集合）      | 增删查复杂度为 O(1)，支持交集、并集、差集等操作           | 共同好友，好友推荐       |
| zset（有序集合） | 增删查复杂度为 O(1)，支持交集、并集、差集等操作，自动排序 | 排行榜，带权重的消息队列 |
| hash（字典）     | 适合存储对象                                              | 存储、读取、修改用户属性 |



## string

string 是最简单的类型，一个 Key 对应一个 Value。

> 💬说明</font>：一个键最大可存储<font color="red"> 512 MB</font>。

### SET *key value*

设置 key 关联的字符串值

- 如果 key 存在，则更新 value；
- 如果 key 不存在，则创建 key 并且更新 value。

```shell
# SET key value

127.0.0.1:6379> SET redis 2021
OK
127.0.0.1:6379> GET redis
"2021"
```



### GET *key*

获取 key 关联的字符串值

- 如果 key 存在，则返回 key 关联的字符串值；
- 如果 key 不存在，则返回 `nil`。

```shell
# GET key

127.0.0.1:6379> GET redis
(nil)
127.0.0.1:6379> SET redis 2021
OK
127.0.0.1:6379> GET redis
"2021"
```



### MSET *key value [key value ...]*

设置一个或多个 Key-Value 键值对

- 如果 key 存在，则更新 value；
- 如果 key 不存在，则创建 key 并且更新 value。

```shell
# MSET key value [key value ...]

127.0.0.1:6379> MSET year 2022 month 1 date 6
OK
127.0.0.1:6379> GET year
"2022"
127.0.0.1:6379> GET month
"1"
127.0.0.1:6379> GET date
"6"
```



### MGET *key [key ...]*

获取一个或多个 Key-Value 键值对

- 如果 key 存在，则返回 key 关联的字符串值；
- 如果 key 不存在，则返回 `nil`。

```shell
# MGET key [key ...]

127.0.0.1:6379> MSET year 2022 month 1 date 6
OK
127.0.0.1:6379> GET year
"2022"
127.0.0.1:6379> GET month
"1"
127.0.0.1:6379> GET date
"6"
127.0.0.1:6379> MGET year month date redis
1) "2022"
2) "1"
3) "6"
4) (nil)
```



### INCR *key*

将 key 关联的数字值加 1

- 如果 key 存在，则判断 key 关联的值是否为数字？
  - 如果为数字值，则加 1；
  - 如果不为数字值，则返回`(error) ERR value is not an integer or out of range`。
- 如果 key 不存在，则创建 key 并且初始化为 0，再加 1。

```shell
# INCR key

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> INCR redis
(error) ERR value is not an integer or out of range
127.0.0.1:6379> GET year
(nil)
127.0.0.1:6379> INCR year
(integer) 1
127.0.0.1:6379> INCR year
(integer) 2
```



### DECR *key*

将 key 关联的数字值减 1

- 如果 key 存在，则判断 key 关联的值是否为数字？
  - 如果为数字值，则减 1；
  - 如果不为数字值，则返回`(error) ERR value is not an integer or out of range`。
- 如果 key 不存在，则创建 key 并且初始化为 0，再减 1。

```shell
# DECR key

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DECR redis
(error) ERR value is not an integer or out of range
127.0.0.1:6379> DECR year
(integer) -1
127.0.0.1:6379> DECR year
(integer) -2
```



### INCRBY *key increment*

将 key 关联的数字值加 `increment`

- 如果 key 存在，则判断 key 关联的值是否为数字？
  - 如果为数字值，则加 `increment`；
  - 如果不为数字值，则返回`(error) ERR value is not an integer or out of range`。
- 如果 key 不存在，则创建 key 并且初始化为 0，再加 `increment`。

```shell
# INCRBY key increment

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> INCRBY redis 2021
(error) ERR value is not an integer or out of range
127.0.0.1:6379> INCRBY year 2021
(integer) 2021
127.0.0.1:6379> INCRBY year 2021
(integer) 4042
```



### DECRBY *key decrement*

将 key 关联的数字值减 `decrement`

- 如果 key 存在，则判断 key 关联的值是否为数字？
  - 如果为数字值，则减 `decrement`；
  - 如果不为数字值，则返回`(error) ERR value is not an integer or out of range`。
- 如果 key 不存在，则创建 key 并且初始化为 0，再减 `decrement`。

```shell
# DECRBY key increment

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DECRBY redis 2021
(error) ERR value is not an integer or out of range
127.0.0.1:6379> DECRBY year 2021
(integer) -2021
127.0.0.1:6379> DECRBY year 2021
(integer) -4042
```



## list

list 是一个双向链表结构，按照插入顺序排序。

> 💬说明</font>：每个 list 最大可存储<font color="red">  `2^32 - 1` </font>个元素。

### LPUSH *key element [element ...]*

将一个或多个值插入列表 Key 的表头（最左边）

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则插入元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则创建 key 并插入元素。

```shell
# LPUSH key [element ...]

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> LPUSH redis redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> LPUSH year 2021 2022
(integer) 2
127.0.0.1:6379> LPUSH year 2023 2024
(integer) 4
```



举个栗子🌰

```shell
# LPUSH key element ...
# RPUSH key element ...
# LRANGE key start stop

# 从右边插入元素 1
127.0.0.1:6379> RPUSH redis 1
(integer) 1
127.0.0.1:6379> LRANGE redis 0 100
1) "1"
# 从右边插入元素 2
127.0.0.1:6379> RPUSH redis 2
(integer) 2
127.0.0.1:6379> LRANGE redis 0 100
1) "1"
2) "2"
# 从左边插入元素 0
127.0.0.1:6379> LPUSH redis 0
(integer) 3
127.0.0.1:6379> LRANGE redis 0 100
1) "0"
2) "1"
3) "2"
```



## set

set 是 string 类型的无序集合；set 通过哈希表实现的，所以增删查的复杂度都是<font color="purple"> O(1)</font>。

> 💬说明</font>：每个 set 最大可存储<font color="red">  `2^32 - 1` </font>个成员。

> 💬说明</font>：set 中每个成员具有<font color="red">  `唯一性` </font>（自动去重）。

- 举个栗子🌰

```shell
# SADD key member ...
# SMEMBERS key

# 添加成员 1
127.0.0.1:6379> SADD redis 1
(integer) 1
# 添加成员 2
127.0.0.1:6379> SADD redis 2
(integer) 1
# 添加成员 0
127.0.0.1:6379> SADD redis 0
(integer) 1
# 添加成员 1（自动去重，返回 0）
127.0.0.1:6379> SADD redis 1
(integer) 0
127.0.0.1:6379> SMEMBERS redis
1) "0"
2) "1"
3) "2"
```



## zset

zset 是有序的 set；但与 set 不同的是，zset 中的每个成员都会关联一个double 类型的 `score`（Redis 根据`score`值对成员进行从小到大的排序）。

> 💬说明</font>：每个 zset 最大可存储<font color="red">  `2^32 - 1` </font>个成员。

> 💬说明</font>：zset 中每个成员具有<font color="red">  `唯一性` </font>（自动去重），但<font color="red"> 每个 score 可以重复</font>。

- 举个栗子🌰

```shell
# ZADD key score member ...
# ZRANGEBYSCORE key min max

127.0.0.1:6379> ZADD redis 0 0
(integer) 1
127.0.0.1:6379> ZADD redis 0 1
(integer) 1
127.0.0.1:6379> ZADD redis 0 2
(integer) 1
127.0.0.1:6379> ZADD redis 0 2
(integer) 0
127.0.0.1:6379> ZRANGEBYSCORE redis 0 100
1) "0"
2) "1"
3) "2"
```



## hash

hash 是一个 string 类型的键值对（field：Value）集合，适用于存储对象。

> 💬说明</font>：每个 hahs 最大可存储<font color="red">  `2^32 - 1` </font>个键值对。

> 💬说明：hash 类似于 Java 中的 `map`。

- 举个栗子🌰

```shell
# HSET key field value ...
# HMSET key field value ...
# HGET key field

# 添加 0：1
127.0.0.1:6379> HSET redis 0 1
(integer) 1
# 更新 field=0 的值
127.0.0.1:6379> HSET redis 0 2
(integer) 0
# 添加 1：2
127.0.0.1:6379> HSET redis 1 2
(integer) 1
# 添加 2：3
127.0.0.1:6379> HSET redis 2 3
(integer) 1
127.0.0.1:6379> HGET redis 0
"2"
127.0.0.1:6379> HGET redis 1
"2"
127.0.0.1:6379> HGET redis 2
"3"
```
