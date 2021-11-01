<!-- title: 【今日份学习】何为 Token？ -->
<!-- date: 2021-10-29 18:13:21 -->
<!-- Table of Content -->

[TOC]



## 问题引入

在没有 token 情况下，每当客户端（Client）向服务端（Server）发送请求数据，服务端（Server）都会进行以下操作，会占用大量的服务器资源：

- 查询数据库的 `username`/`password`
- 比对 `username`/`password` 是否正确，并作出响应



## 技术定义

服务端（Server）生成的字符串，以作为客户端（Client）进行请求的**访问令牌**。

- 第一次登陆（客户端）
  - 服务端生成一个 Token
  - 将 Token 返回给客户端
- 下一次登陆（客户端）
  - 只需携带 Token 即可，无需携带 `username`/`password`



## 使用目的

减轻服务端的压力，减少频繁地查询数据库，使服务端更加健壮。



## Token 定义

- <font color="purple">**设备号**</font>
- <font color="purple">**设备 MAC 地址**</font>
- <font color="purple">**session 值**</font>