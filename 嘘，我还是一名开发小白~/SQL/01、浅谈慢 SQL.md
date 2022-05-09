<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-02-22 13:47:16 -->

[TOC]

---

## 什么是慢 SQL？

慢 SQL 是指**查询时间超过时间阈值（long_query_time）**的 SQL 语句，会记录到慢查询日志中。



## 如何设置慢 SQL 服务？

- **查询慢 SQL 日志服务**

  ```sql
  SHOW VARIABLES LIKE '%slow_query_log%';
  ```

  

- **开启慢 SQL 日志服务**

  ```sql
  SET GLOBAL slow_query_log = 1;
  ```

  > **💬说明**：慢 SQL 日志服务是默认关闭的。

  

- **查询慢 SQL 的阈值**

  ```sql
  SHOW VARIABLES LIKE 'long_query_time';  
  ```

  

- **设置慢 SQL 的阈值**

  ```sql
  /* 单位：秒 */
  SET GLOBAL long_query_time = 10;
  ```

  > **💬说明**：设置不生效时，开启一个新窗口试试。

  

- **查询慢 SQL 的语句数量**

  ```sql
  SHOW GLOBAL STATUS LIKE '%Slow_queries%';
  ```



## 如何分析慢 SQL 日志？

```shell
/usr/local/mysql/bin/mysqld, Version: 8.0.25 (MySQL Community Server - GPL). started with:
Tcp port: 3306  Unix socket: /tmp/mysql.sock
Time                 Id Command    Argument
## 日志记录时间
// Time: 2022-02-22T06:24:35.295573Z
## 登录用户，主机地址
// User@Host: root[root] @ localhost [127.0.0.1]  Id:    13
## Query_time 为查询时间，Lock_time 为锁表时间，Rows_sent 为返回的行数，Rows_examined 为扫描的行数
// Query_time: 1.505517  Lock_time: 0.000000 Rows_sent: 1  Rows_examined: 1
## SQL 语句
use mysql;
SET timestamp=1645511073;
/* ApplicationName=DataGrip 2021.3.4 */ SELECT  SLEEP(1.5);
```



## 导致慢 SQL 的原因有哪些？

- SQL 编写问题
- 锁
- 业务实例对 IO/CPU等资源的争用
- 服务器配置
- 数据库 Bug

