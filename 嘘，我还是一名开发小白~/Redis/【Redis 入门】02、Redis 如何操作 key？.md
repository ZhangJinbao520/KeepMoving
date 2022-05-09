<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-01-06 11:48:18 -->

[TOC]

---

## 1. DEL *key [key ...]*

> - 起始版本：<font color="blue">**1.0.0**</font>
> - 时间复杂度：<font color="purple">**$O(N)——N 为 key 的数量$**</font>

删除一个或多个指定的 key。

- 当删除一个时：
  - 如果 key 存在，则返回 1；

  - 如果 key 不存在，则返回 0（忽略）。
- 当删除多个时：

  - 返回成功删除 key 的个数。

### 返回值（return）

[integer-reply](http://www.redis.cn/topics/protocol.html#integer-reply)： 成功被删除的 key 的数量。



### 举个栗子🌰

```shell
# DEL key [key ...]

# 删除一个
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> DEL redis
(integer) 0
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> DEL redis
(integer) 1

# 删除多个
127.0.0.1:6379> MSET redis redis year 2022
OK
127.0.0.1:6379> KEYS *
1) "redis"
2) "year"
127.0.0.1:6379> DEL redis year month
(integer) 2
```



## 2. DUMP *key*

> - 起始版本：<font color="blue">**2.6.0**</font>
> - 时间复杂度：<font color="purple">**$O(1)+O(N*M)——N 为值对象数量、M 为（平均）值对象大小$**</font>

序列化指定 key 的值，并返回被序列化的值；其序列化后的特点为：

- 自带 64 位校验和
- 值的编码格式和 RDB 文件保持一致

> ***💬说明：*** *如果 Redis 版本之间使用的 RDB 不兼容，那么反序列化会失败。*

### 返回值（return）

- 如果 key 存在，则返回序列化后的值；
- 如果 key 不存在，则返回 `nil`。



### 举个栗子🌰

```shell
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> DUMP redis
(nil)
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> DUMP redis
"\x00\x05redis\t\x00\x15\xa2\xf8=\xb6\xa9\xde\x90"
```



## 3. EXISTS *key [key ...]*

> - 起始版本：<font color="blue">**1.0.0**</font>
> - 时间复杂度：<font color="purple">**$O(1)$**</font>

判断 key 是否存在。

- 当判断一个时：
  - 如果 key 存在，则返回 1；

  - 如果 key 不存在，则返回 0。
- 当判断多个时：

  - 返回 key 存在的个数。

### 返回值

[integer-reply](http://www.redis.cn/topics/protocol.html#integer-reply)：返回 key 存在的个数。



### 举个栗子🌰

```shell
127.0.0.1:6379> KEYS *
1) "redis"
127.0.0.1:6379> EXISTS redis
(integer) 1
127.0.0.1:6379> EXISTS redis year month
(integer) 1
127.0.0.1:6379> SET year 2022
OK
127.0.0.1:6379> EXISTS redis year month
(integer) 2
```



## EXPIRE *key seconds*

> - 起始版本：<font color="blue">**1.0.0**</font>
> - 时间复杂度：<font color="purple">**$O(1)$**</font>

设置 Key 的过期时间（单位：秒）。

- 如果 Key 存在，则返回 1（设置成功）；
- 如果 Key 不存在，则返回 0（设置失败）。











### KEYS *pattern*

查看所有的 Key（正则匹配）。

- 如果 Key 为空，则返回`(empty array)`；
- 如果 Key 不为空，则返回 Key 列表；

```shell
# KEYS pattern

127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> KEYS *
1) "redis"
```







### EXPIRE *key seconds*

设置 Key 的过期时间（单位：秒）。

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
127.0.0.1:6379> TTL redis
(integer) 5
# 等待 5 秒
127.0.0.1:6379> GET redis
(nil)

# Key 不存在
127.0.0.1:6379> EXPIRE redis 5
(integer) 0
```



### TTL *key*

查看 Key 的过期时间。

- 如果 Key 存在，则返回 Key 的过期时间（单位：秒）；

  > ***💬说明：*** *<font color="red">`-1`表示永不过期。</font>*

- 如果 Key 不存在，则返回`-2`。

```shell
# TTL key

# Key 不存在
127.0.0.1:6379> KEYS *
(empty array)
127.0.0.1:6379> TTL redis
(integer) -2

# Key 存在
127.0.0.1:6379> SET redis redis
OK
127.0.0.1:6379> TTL redis
(integer) -1
```



### FLUSHALL

清空 Redis 服务器的所有数据。

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

清空当前数据库的所有数据。

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

选择数据库，index ∈ [0, 15]。

```shell
# SELECT index

127.0.0.1:6379> SELECT 1
OK
127.0.0.1:6379[1]> SELECT 15
OK
127.0.0.1:6379[15]> 
```
