<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-03-08 11:10:49 -->

[TOC]

---

## JSON 是什么？

[**JSON**](http://json.org/json-zh.html)（**J**ava**S**rcipt **O**bject **N**otation，JavaScript 对象表示法）是一种与开发语言无关、轻量级的==**数据格式**==。



## JSON 发展史

- 2000 年

  > Douglas Crockford（道格拉斯·克罗克福特）发明了 JSON，并于 2001 年开始推广使用。

- 2005 ~ 2006 年

  > JSON 正式成为主流的数据格式。

- 2013 年

  > ECMA International（欧洲计算机制造商协会）制定了 JSON 的语法标准——[ECMA-404](https://www.ecma-international.org/publications-and-standards/standards/ecma-404)。



## JSON 优劣势

- 优势

  - **易于人的阅读和编写**
  - **易于程序解析和生成**
  - **读写速率快**
- 劣势

  - **单一的数值类型**

  - **不支持日期类型**

    > ***💬说明：*** *当前一般解决方案是采用**日期字符串**或**时间戳**格式。*

  - **不支持注释**



## JSON 应用场景

JSON 是行业内使用最为广泛的数据传输格式。

- **定义接口**
  
  - Ajax（**A**synchronous **J**avascript **A**nd **X**ML，异步 JavaScript 和 XML）

  - RPC（**R**emote **P**rocedure **C**all，远程过程调用）

  - 后端返回的数据

  - 开放 API

  - …

- **序列化**

  > ***💬说明：*** *将程序中的对象转换为可保存或可传输的数据。*

- **生成 Token**

- **配置文件**

  - npm

  - …



## JSON 数据结构

### Object（对象）

“名称/值”对的集合（A collection of name/value pairs）。




### Array（数组）

值的有序列表（An ordered list of values）。



## JSON 值

JSON 值可以是：

- **字符串**

- **数值**

- **对象**

- **数组**

- **布尔**

- **null**

<div align="center">
<img src="https://www.json.org/img/value.png" />
</div>

### 字符串

字符串是由双引号（**`""`**）包围的任意数量 Unicode 字符的集合，使用反斜线（`\`）转义。

<div align="center">
<img src="https://www.json.org/img/string.png" />
</div>

- 代码示例

```json
[
    {
        "name": "小 Z",
        "age": 18
    }
]
```



### 数值

数值可以是：

- 整数

- 浮点数

- 指数（`E`/`e`）

<div align="center">
<img src="https://www.json.org/img/number.png" />
</div>

- 代码示例

```json
[
    {
        "name": "小 Z",
        "age": 18
    },
    {
        "name": "小 Z",
        "age": 18.0
    },
    {
        "name": "小 Z",
        "age": 1.8E1
    }
]
```



### 对象

对象是以左花括号（`{`）开始，右花括号（`}`）结束。

<div align="center">
<img src="https://www.json.org/img/object.png" />
</div>

- 代码示例

```json
{
    "name": "小 Z",
    "age": 18
}
```



### 数组

数组以左中括号（`[`）开始，右中括号（`]`）结束。。

<div align="center">
<img src="https://www.json.org/img/array.png" />
</div>

- 代码示例

```json
[
    {
        "name": "小 Z",
        "age": 18
    },
    {
        "name": "小 C",
        "age": 18
    }
]
```



### 布尔

布尔值可以是：

- **true**

- **false**

```json
"married": false
```



### null

JSON 值可以是 `null`。

```json
"flags": null
```



## JSON 与 Python

### 解码

| <span style="display:inline-block;width: 400px">JSON</span> | <span style="display:inline-block;width: 400px">Python</span> |
| :---------------------------------------------------------: | :----------------------------------------------------------: |
|                           object                            |                             dict                             |
|                            array                            |                             list                             |
|                           string                            |                             str                              |
|                         number(int)                         |                             int                              |
|                        number(real)                         |                            float                             |
|                            true                             |                             True                             |
|                            false                            |                            False                             |
|                            null                             |                             None                             |



### 编码

| <span style="display:inline-block;width: 400px">Python</span> | <span style="display:inline-block;width: 400px">JSON</span> |
| :----------------------------------------------------------: | :---------------------------------------------------------: |
|                             dict                             |                           object                            |
|                         list, tuple                          |                            array                            |
|                             str                              |                           string                            |
|            int, float, int- & float-derived Enums            |                           number                            |
|                             True                             |                            true                             |
|                            False                             |                            false                            |
|                             None                             |                            null                             |
