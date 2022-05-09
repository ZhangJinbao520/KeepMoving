<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-01-06 11:48:18 -->

[TOC]

---

## Redis 数据类型

Redis 可提供五种数据类型：<font color="purple">**STRING、LIST、SET、ZSET、HASH**</font>。

| <span style="display:inline-block;width: 100px">类型</span> | <span style="display:inline-block;width: 100px">特性</span> | <span style="display:inline-block;width: 100px">适用场景</span> |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| **STRING**                                                  | 可以包含任意数据                                            | N/A                                                          |
| **LIST**                                                    | 增删快                                                      | 时间线，消息队列                                             |
| **SET**                                                     | 增删查复杂度为 O(1)，支持交集、并集、差集等操作             | 共同好友，好友推荐                                           |
| **ZSET**                                                    | 增删查复杂度为 O(1)，支持交集、并集、差集等操作，自动排序   | 排行榜，带权重的消息队列                                     |
| **HASH**                                                    | 适合存储对象                                                | 存储、读取、修改用户属性                                     |



## String

string 是最简单的类型，一个 Key 对应一个 Value。

> ***💬说明：*** *一个键最大可存储 ==**512 MB**==。*

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



## List

list 是一个双向链表结构，按照插入顺序排序。

> ***💬说明：*** *每个 list 最大可存储 ==**2^32^ - 1**== 个元素。*

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
127.0.0.1:6379> LPUSH redis 1
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> LPUSH year 1
(integer) 1
127.0.0.1:6379> LPUSH year 2
(integer) 2
127.0.0.1:6379> LPUSH year 3
(integer) 3
127.0.0.1:6379> LPUSH year 4
(integer) 4
127.0.0.1:6379> LRANGE year 0 -1
1) "4"
2) "3"
3) "2"
4) "1"
```

### LRANGE *key start stop*

获取指定区间内的列表元素

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则返回列表元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`(empty array)`。

> ***💬说明：*** *如果需要查询所有，指定 ==**stop=-1**== 即可。*

```shell
# LRANGE key start stop

127.0.0.1:6379> LPUSH year 1 2 3 4
(integer) 4
127.0.0.1:6379> LRANGE year 0 -1
1) "4"
2) "3"
3) "2"
4) "1"
127.0.0.1:6379> SET year 2021
OK
127.0.0.1:6379> LRANGE year 0 -1
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> LRANGE Redis 0 -1
(empty array)
```

### RPUSH *key element [element ...]*

将一个或多个值插入列表 Key 的表尾（最右边）

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则插入元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则创建 key 并插入元素。

```shell
# RPUSH key [element ...]

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> RPUSH redis 1
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> RPUSH year 1
(integer) 1
127.0.0.1:6379> RPUSH year 2
(integer) 2
127.0.0.1:6379> RPUSH year 3
(integer) 3
127.0.0.1:6379> RPUSH year 4
(integer) 4
127.0.0.1:6379> LRANGE year 0 -1
1) "1"
2) "2"
3) "3"
4) "4"
```

### LPOP *key*

移除并返回列表 Key 的表头元素（最左边）

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则移除并返回列表 Key 的表头元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`nil`。

```shell
# LPOP key

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> LPOP redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> LPUSH year 1
(integer) 1
127.0.0.1:6379> LPOP year
"1"
127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> LPOP year
(nil)
```

### RPOP *key*

移除并返回列表 Key 的表尾元素（最右边）

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则移除并返回列表 Key 的表尾元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`nil`。

```shell
# RPOP key

127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> RPOP redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> RPUSH year 1
(integer) 1
127.0.0.1:6379> RPOP year
"1"
127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> RPOP year
(nil)
```

### LREM *key count element*

移除指定 `count` 个与`element`相等列表 Key 的元素

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则判断 count 是否大于 0？
    - 如果 count > 0，则从表头开始向表尾搜索，移除并返回移除成功个数；
    - 如果 count < 0，则从表尾开始向表头搜索，移除并返回移除成功个数。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`0`。

```shell
# LREM key count element

127.0.0.1:6379> LPUSH redis 1 2 2 3 3 3
(integer) 6
127.0.0.1:6379> LRANGE redis 0 -1
1) "3"
2) "3"
3) "3"
4) "2"
5) "2"
6) "1"
127.0.0.1:6379> LREM redis 2 1
(integer) 1
127.0.0.1:6379> LREM redis 2 2
(integer) 2
127.0.0.1:6379> LREM redis 2 3
(integer) 2
127.0.0.1:6379> LRANGE redis 0 -1
1) "3"
127.0.0.1:6379> DEL redis
(integer) 1
127.0.0.1:6379> LREM redis 2 redis
(integer) 0
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> LREM redis 2 1
(error) WRONGTYPE Operation against a key holding the wrong kind of value
```

### LINDEX *key index*

返回 Key 列表下标为 index 的元素

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则返回列表 Key 下标为 index 的元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`nil`。

```shell
# LINDEX key index

127.0.0.1:6379> LPUSH redis 1 2 2 3 3 3
(integer) 6
127.0.0.1:6379> LINDEX redis 0
"3"
127.0.0.1:6379> LINDEX redis 1
"3"
127.0.0.1:6379> LINDEX redis 2
"3"
127.0.0.1:6379> LINDEX redis 3
"2"
127.0.0.1:6379> LINDEX redis 4
"2"
127.0.0.1:6379> LINDEX redis 5
"1"
127.0.0.1:6379> LINDEX redis 6
(nil)
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> LINDEX redis 0
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> DEL redis
(integer) 1
127.0.0.1:6379> LINDEX redis 0
(nil)
```

### LTRIM *key start stop*

修剪列表，保留范围内的元素（删除范围外的元素）

- 如果 Key 存在，则判断 key 关联的值是否为列表？
  - 如果是，则修剪列表，保留范围内的元素；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`OK`。

```shell
# LTRIM key start stop

127.0.0.1:6379> LPUSH redis 1 2 2 3 3 3
(integer) 6
127.0.0.1:6379> LRANGE redis 0 -1
1) "3"
2) "3"
3) "3"
4) "2"
5) "2"
6) "1"
127.0.0.1:6379> LTRIM redis 0 2
OK
127.0.0.1:6379> LRANGE redis 0 -1
1) "3"
2) "3"
3) "3"
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> LTRIM redis 0 2
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> DEL redis
(integer) 1
127.0.0.1:6379> LTRIM redis 0 2
OK
```

### 如何利用 Redis 实现栈和队列？

- list 控制同一边进，同一边出即为==**栈**==；
- list 控制一边进，另一边出即为==**队列**==。



## Set

set 是 string 类型的无序集合；set 通过哈希表实现的，所以增删查的复杂度都是<font color="purple"> O(1)</font>。

set集合是一个无序的不含重复值的队列

> ***💬说明：*** *每个 set 最大可存储 ==**2^32^ - 1**== 个成员。*

> ***💬说明：*** *set 中每个成员具有<font color="red">  `唯一性` </font>（自动去重）。*

### SADD *key member [member ...]*

将一个或多个`member`元素添加到集合 set 中

- 如果 Key 存在，则判断 key 关联的值是否为集合？
  - 如果是，则判断集合的`member`是否已存在？
    - 如果`member`存在，则忽略；
    - 如果`member`不存在，则添加。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则创建集合 set 并返回添加成功个数。

```shell
# SADD key member [member ...]

127.0.0.1:6379> SADD redis 1 2 3 4
(integer) 4
127.0.0.1:6379> SADD redis 1 2 3 4 5
(integer) 1
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> SADD redis 1 2 3 4 5
(error) WRONGTYPE Operation against a key holding the wrong kind of value
```

### SMEMBERS *key*

返回集合 key 中的所有成员

- 如果 Key 存在，则判断 key 关联的值是否为集合？
  - 如果是，则返回集合 Key 的所有成员；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`(empty array)`。

```shell
# SMEMBERS key

127.0.0.1:6379> SADD redis 1 2 3
(integer) 3
127.0.0.1:6379> SMEMBERS redis
1) "1"
2) "2"
3) "3"
127.0.0.1:6379> SMEMBERS year
(empty array)
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> SMEMBERS redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
```

### SREM *key member [member ...]*

移除集合 Key 中的一个或多个元素

- 如果 Key 存在，则判断 key 关联的值是否为集合？
  - 如果是，则判断`member`是否存在？
    - 如果存在，则移除；
    - 如果不存在，则忽略。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`0`。

```shell
# SREM key member [member ...]

127.0.0.1:6379> SADD redis 1 2 3 4
(integer) 4
127.0.0.1:6379> SREM redis 0 1 2 3
(integer) 3
127.0.0.1:6379> SMEMBERS redis
1) "4"
127.0.0.1:6379> SET year 2022
OK
127.0.0.1:6379> SREM year 2022
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> SREM month 2022
(integer) 0
```

### SCARD *key*

返回集合 Key 的元素数量

- 如果 Key 存在，则判断 key 关联的值是否为集合？
  - 如果是，则返回集合 Key 的长度；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 Key 不存在，则返回`0`。

```shell
# SCARD key

127.0.0.1:6379> SADD redis 1 2 2 3 3 3
(integer) 3
127.0.0.1:6379> SMEMBERS redis
1) "1"
2) "2"
3) "3"
127.0.0.1:6379> SCARD redis
(integer) 3
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> SCARD redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> DEL redis
(integer) 1
127.0.0.1:6379> SCARD redis
(integer) 0
```

### SDIFF *key [key]*

返回集合 Key 与指定集合之间的差集

```shell
# SDIFF key [key]

127.0.0.1:6379> SADD redis 1 2 3
(integer) 3
127.0.0.1:6379> SADD year 1 2021
(integer) 2
127.0.0.1:6379> SDIFF redis year
1) "2"
2) "3"
```





## Zset

zset 是有序的 set；但与 set 不同的是，zset 中的每个成员都会关联一个double 类型的 `score`（Redis 根据`score`值对成员进行从小到大的排序）。

> 💬说明</font>：每个 zset 最大可存储 ==**2^32^ - 1**== 个成员。

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



## Hash

hash 是一个 string 类型的键值对（field：Value）集合，适用于存储对象。

> 💬说明</font>：每个 hahs 最大可存储 ==**2^32^ - 1**== 个键值对。

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

