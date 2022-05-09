<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-01-06 11:48:18 -->

[TOC]

---

## 1. APPEND *key value*

> - 起始版本：<font color="blue">**2.0.0**</font>
> - 时间复杂度：<font color="purple">**$O(1)$**</font>

- 如果 key 已存在，则判断值类型是否为字符串？
  - 如果是，则将 value 添加值原值的结尾；
  - 如果不是，则<font color="red">**报错**</font>。
- 如果 key 不存在，则先创建一个**空字符串的 key**，在执行追加操作。



### 返回值（return）

[Integer reply](http://www.redis.cn/topics/protocol.html#integer-reply)：返回 append 后字符串值（value）的长度。



### 举个栗子🌰

```shell
# Key 不存在
127.0.0.1:6379> EXISTS redis
(integer) 0
127.0.0.1:6379> APPEND redis 1
(integer) 1
127.0.0.1:6379> GET redis
"1"
# Key 存在
127.0.0.1:6379> APPEND redis 2
(integer) 2
127.0.0.1:6379> GET redis
"12"
127.0.0.1:6379> FLUSHALL
OK
# Key 为非字符串
127.0.0.1:6379> LPUSH redis 0
(integer) 1
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> APPEND redis 1
(error) WRONGTYPE Operation against a key holding the wrong kind of value
```



## SET *key value*

设置 key 关联的字符串值。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则更新 value；
  - 如果不是，则删除原 key 后创建新 Key 并更新 value。

- 如果 key 不存在，则创建 key 并更新 value。

```shell
# SET key value

# Key 存在
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> GET redis
"redis"

# Key 不存在
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> SET redis 2021
OK
127.0.0.1:6379> GET redis
"2021"
```



### GET *key*

获取 key 关联的字符串值。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，返回 key 关联的字符串值；
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。

- 如果 key 不存在，则返回 `nil`。

```shell
# GET key

# Key 存在
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> GET redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> SET redis 2021
OK
127.0.0.1:6379> GET redis
"2021"

# Key 不存在
127.0.0.1:6379> GET redis
(nil)
```



### MSET *key value [key value ...]*

设置一个或多个 Key-Value 键值对。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则更新 value；
  - 如果不是，则删除原 key 后创建新 Key 并更新 value。
- 如果 key 不存在，则创建 key 并更新 value。

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

获取一个或多个 Key-Value 键值对。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，返回 key 关联的字符串值；
  - 如果不是，则返回 `nil`。
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
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> MGET year month date redis
1) "2022"
2) "1"
3) "6"
4) (nil)
```



### INCR *key*

将 key 关联的数值加 1。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则判断 key 关联值的编码类型是否为 `INT`？
    - 如果是，则加 1；
    - 如果不是，则返回`(error) ERR value is not an integer or out of range`。

  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。

- 如果 key 不存在，则创建 key 并初始化为 0，再加 1。

```shell
# INCR key

# Key 存在
## INT
127.0.0.1:6379> GET redis
"2"
127.0.0.1:6379> INCR redis
(integer) 3
## 非 INT
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> INCR redis
(error) ERR value is not an integer or out of range
## 非 String
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> INCR redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value

# Key 不存在
127.0.0.1:6379> TYPE redis
none
127.0.0.1:6379> INCR redis
(integer) 1
127.0.0.1:6379> GET redis
"1"
```



### DECR *key*

将 key 关联的数字值减 1。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则判断 key 关联值的编码类型是否为 `INT`？
    - 如果是，则减 1；
    - 如果不是，则返回`(error) ERR value is not an integer or out of range`。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 key 不存在，则创建 key 并初始化为 0，再减 1。

```shell
# DECR key

# Key 存在
## INT
127.0.0.1:6379> GET redis
"1"
127.0.0.1:6379> DECR redis
(integer) 0
## 非 INT
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DECR redis
(error) ERR value is not an integer or out of range
## 非 String
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> DECR redis
(error) WRONGTYPE Operation against a key holding the wrong kind of value

# Key 不存在
127.0.0.1:6379> TYPE redis
none
127.0.0.1:6379> DECR redis
(integer) -1
127.0.0.1:6379> GET redis
"-1"
```



### INCRBY *key increment*

将 key 关联的数字值加 `increment`。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则判断 key 关联值的编码类型是否为 `INT`？
    - 如果是，则加 `increment`；
    - 如果不是，则返回`(error) ERR value is not an integer or out of range`。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 key 不存在，则创建 key 并初始化为 0，再加 `increment`。

```shell
# INCRBY key increment

# Key 存在
## INT
127.0.0.1:6379> GET redis
"2"
127.0.0.1:6379> INCRBY redis 2020
(integer) 2022
## 非 INT
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> INCRBY redis 2020
(error) ERR value is not an integer or out of range
## 非 String
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> INCRBY redis 2020
(error) WRONGTYPE Operation against a key holding the wrong kind of value

# Key 不存在
127.0.0.1:6379> TYPE redis
none
127.0.0.1:6379> INCRBY redis 2020
(integer) 2020
127.0.0.1:6379> GET redis
"2020"
```



### DECRBY *key decrement*

将 key 关联的数字值减 `decrement`。

- 如果 key 存在，则判断 key 关联值的类型是否为 `STRING`？
  - 如果是，则判断 key 关联值的编码类型是否为 `INT`？
    - 如果是，则减 `decrement`；
    - 如果不是，则返回`(error) ERR value is not an integer or out of range`。
  - 如果不是，则返回`(error) WRONGTYPE Operation against a key holding the wrong kind of value`。
- 如果 key 不存在，则创建 key 并初始化为 0，再减 `decrement`。

```shell
# DECRBY key decrement

# Key 存在
## INT
127.0.0.1:6379> GET redis
"1"
127.0.0.1:6379> DECRBY redis 2020
(integer) -2019
## 非 INT
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DECRBY redis 2020
(error) ERR value is not an integer or out of range
## 非 String
127.0.0.1:6379> TYPE redis
list
127.0.0.1:6379> DECRBY redis 2020
(error) WRONGTYPE Operation against a key holding the wrong kind of value

# Key 不存在
127.0.0.1:6379> TYPE redis
none
127.0.0.1:6379> DECRBY redis 2020
(integer) -2020
127.0.0.1:6379> GET redis
"-2020"
```

