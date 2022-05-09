<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-02-22 19:35:35 -->

[TOC]

---

## 什么是 TTFB？

TTFB（Time To First Byte）是指从“打开网页”到“网页内容开始呈现”之间的等待时间。

> Time spent waiting for the initial response, also known as the Time To First Byte. This time captures the latency of a round trip to the server in addition to the time spent waiting for the server to deliver the response.

- **浏览器发送 HTTP 请求的时间**

  - DNS 查询时间

  - 网络速率

  - …

- **服务器处理 HTTP 请求的时间**

  - 程序启动

  - 数据库调用

  - 脚本运行

  - 与其他系统通信

  - …

- **服务器将响应的第一个字节发送回浏览器的时间**

  - 网络速率

  - …

  > ***💬说明：*** *通过网络传输请求和响应的响应时间约占 TTFB 的 40%。*

