<!-- @author: Zhang Jinbao -->

<!-- @date: 2021-12-22 10:37:29 -->

[TOC]

---

## 为撒子要区分前端/后端 Bug？

在中国社会，当 Bug 不能明确是归属谁的时候，大家会采取踢皮球形式踢来踢去，从而导致沟通成本增加、Bug 解决延误等问题，毕竟谁会主动承认自己的错误呢！



## 前端/后端 Bug 各有何特点?

| <span style="display:inline-block;width: 100px">前端 Bug</span> | <span style="display:inline-block;width: 100px">后端Bug</span> |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                           界面相关                           |                         业务逻辑相关                         |
|                           布局相关                           |                           性能相关                           |
|                          兼容性相关                          |                           数据相关                           |
|                           交互相关                           |                          安全性相关                          |



## 如何区分前端/后端Bug？

利用抓包工具，可以从以下几个方面进行分析：

1. <font color="red">**请求接口 URL** </font>是否正确？
   - 正确：可能为后端 Bug

   - 错误：为前端 Bug

2. <font color="red">**接口传参 Payload** </font>是否正确？
   -  正确：可能为后端 Bug
   
   -  错误：为前端 Bug
   
3. <font color="red">**接口响应 Response** </font>是否正确？
   - 正确：为前端 Bug
   
   - 错误：为后端 Bug
   
4. **在浏览器控制台，输入 `JavaScript` 代码进一步调试。**



## 定位 Bug 属于前端还是后端，有什么好办法？

### 1. 接口查看法

绝大多数浏览器都有自带的<font color="blue">**接口查看工具**</font>，包括但不限于：Chrome、FireFox 等，可通过<kbd>F12</kbd>开启开发者模式，在 Network 中可以查看当前页面发送的每个请求。

> ***💬说明：*** *接口查看法是最常用且必须掌握的方法，常用于查看是前端显示错误还是后端数据错误。*



### 2. 日志查看法

当我们发现一个 Bug 并且不确定这个 Bug 属于前端还是后端时，可以查看后端服务日志是否有相关记录？

- 如果有，查看相关日志信息进行下一步分析

- 如果没有，则该功能并未与后端交互，为前端 Bug



### 3. 经验法

经验法是在了解功能实现和业务逻辑的前提下日积月累的。

> ***💬说明：*** *作为一名合格的社狗，应时常学会总结和反思。*



