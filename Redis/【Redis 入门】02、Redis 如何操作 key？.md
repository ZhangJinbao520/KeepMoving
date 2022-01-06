<!-- @title: 【Redis 入门】02、Redis 如何操作 key？ -->
<!-- @date: 2022-01-06 11:48:18 -->
<!-- @author: Zhang Jinbao -->

[TOC]

## Key 操作

### KEYS *pattern*

查看所有的 Key（正则匹配）

- 如果 Key 不为空，则返回 Key 列表；
- 如果 Key 为空，则返回`(empty array)`。

```shell
# KEYS pattern

127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> KEYS *
1) "redis"
```



### DEL *key [key ...]*

删除一个或多个指定的 Key

- 当删除一个时：

  - 如果 Key 存在，则返回 1；

  - 如果 Key 不存在，则返回 0。

- 当删除多个时：

  - 返回删除 Key 成功的个数。

```shell
# DEL key [key ...]

# 删除一个
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> DEL redis
(integer) 0
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DEL redis
(integer) 1
# 删除多个
127.0.0.1:6379> MSET redis redis year 2022
OK
127.0.0.1:6379> DEL redis year
(integer) 2
```



### EXPIRE *key seconds*

设置 Key 的过期时间（单位：秒）

- 如果 Key 存在，则返回 1（设置成功）；
- 如果 Key 不存在，则返回 0（设置失败）。

```shell
# EXPIRE key seconds

# Key 存在
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> GET redis
"redis"
127.0.0.1:6379> EXPIRE redis 5
(integer) 1
127.0.0.1:6379> GET redis
(nil)
# Key 不存在
127.0.0.1:6379> EXPIRE redis 5
(integer) 0
```



### TTL *key*

查看 Key 的过期时间

- 如果 Key 存在，则返回 Key 的过期时间（单位：秒）；

  > 💬说明</font>：`-1`表示永不过期。

- 如果 Key 不存在，则返回 `-2`。

```shell
# TTL key

127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> TTL redis
(integer) -2
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> TTL redis
(integer) -1
```



### FLUSHALL

清空 Redis 服务器的所有数据

```shell
# FLUSHALL

127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> FLUSHALL
OK
127.0.0.1:6379> FLUSHALL
OK
```



### FLUSHDB

清空当前数据库的所有数据

```shell
# FLUSHDB

127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> FLUSHDB
OK
127.0.0.1:6379> KEYS *
(empty array)
# 切换数据库
127.0.0.1:6379> SELECT 1
OK
127.0.0.1:6379[1]> KEYS *
1) "redis"
```



### SELECT *index*

选择数据库，index ∈ [0, 15]

```shell
# SELECT index

127.0.0.1:6379> SELECT 1
OK
127.0.0.1:6379[1]> SELECT 15
OK
127.0.0.1:6379[15]> 
```







