<!-- @title: 【Python】Python 入门基础 -->
<!-- @date: 2021-10-26 12:21:51 -->
<!-- @author: Zhang Jinbao -->

[TOC]

## Python 简介

[Python](http://www.python.org)是由荷兰Guido van Rossum（吉多·范罗苏姆）于 1989 年发明的一种面向对象的程序设计语言，其特点是吸收其他编程语言的各类优点，是一种脚本语言。

像其他语言一样，Python 源代码同样遵循 [GPL（GNU General Public License）](https://www.gnu.org/home.zh-cn.html)协议。

> 💬注意：Python3 不兼容 Python2，但可使用 2to3 工具进行代码转换。



## Python 特点

- 易于学习（关键字较少，结构简单）
- 易于阅读（代码简洁——缩进）
- 面向对象
- 免费开源
- 互动模式（在线调试）
- 丰富的库
- 可移植性（Windows/Linux/MacOS/…）
- 可扩展（多语言共同编写）
- 数据库
- GUI 编程
- 可嵌入（如：嵌入 C#/C++程序）
- …



## Python 可以做什么？

- WEB 开发
  - Django
  - pyramid
  - Tornado
  - Bottle
  - Flask
  - WebPy
  - …
- 网络编程
  - requests
  - Scrapy
  - Twisted
  - Paramiko
  - …
- 科学运算
  - Pandas
  - SciPy
  - IPython
  - …
- GUI 开发
  - WxPython
  - PyQT
  - Kivy
  - …
- 运维自动化
  - OpenStack
  - SaltStack
  - Ansible
  - 腾讯蓝鲸
  - …
- 游戏开发
- 移动设备
- 嵌入式设备
- 云计算
- 人工智能



## 都有谁在用 Python？

- 国内
  - 腾讯
  - 阿里
    - 淘宝
    - …
  - 百度
    - 知乎
    - …
  - 网易
  - 新浪
  - 金山
  - 盛大
  - 土豆
  - 搜狐
  - 果壳
  - 春雨医生
  - …
- 国外
  - NASA（ 美国航天局）
  - CIA（美国中情局）
  - Google
    - Google App Engine
    - code.google.com
    - 谷歌地球
    - 谷歌爬虫
    - 谷歌广告
    - …
  - Facebook
  - YouTube
  - Dropbox
  - Reddit
  - Instagram
  - RedHat
  - …

## Python 编码

默认情况，Python 源代码以 UTF-8 进行编码，所有都是 Unicode 字符。当然也可为源代码执行编码格式，如：

```python
# -*- coding: cp-1252 -*-
```



## Python 标识符

- 首字符必须是`字母`、`_`
- 其他字符可以是`字母`、`数字`、`_`
- 大小写敏感

> 💬注意：在 Python3 中，使用非 ASCII 码定义标识符也是允许的，如：变量_123。

```python
>>> 变量_123 = "非 ASCII 码"
>>> pinrt(变量_123)
非 ASCII 码
```



## Python 保留关键字

任何编程语言都存在保留关键字，它们不能作为任何标识符的名称。

在 Python 标准库中提供了一个 keyword 模块，可输出当前版本的所有关键字，如：

```python
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```



## Python 缩进

Python 使用<font color="purple">缩进</font>来区分代码块。

> 💬注意：缩进未必是 4 空格，同一个代码块的语句必须包含相同的缩进空格数。

```python
if True:
    print(True)
else:
  print(False)  # 缩进不一致，会导致运行错误

# 当运行时，会报如下错误
IndentationError: unindent does not match any outer indentation level
```



## Python 注释

单行注释使用`#`，多行注释可使用`#`、或`'''`、或`"""`。

```python
# 单行注释

# 多行注释一
# 多行注释一

'''
多行注释二
多行注释二
'''

"""
多行注释三
多行注释三
"""
if __name__ == '__main__':
    pass
```



## Python 变量定义

在 Python 中，<font color="red">变量无需预先声明</font>；当且仅当变量被赋值后，才会创建变量（本质为创建对象）。

Python 支持单个、多个变量同时赋值，如：

```python
# 单个变量
>>> a = 1
>>> print(a)
1

# 多个变量
>>> a = b = 2
>>> print(a, b)
2 2
>>> a, b, c = 3, 4, "True"
>>> print(a, b, c)
3 4 True
```



## Python 数据类型

在 Python 中，共有 8 种数据类型，分别是：

- bool（布尔）
- int（整数）
- float（浮点数）
- complex（复数）
- str（字符串）
- tuple（元组）
- list（列表）
- set（集合）
- dict（字典）

> 💬注意：其中bool、int、float、str、tuple 为<font color="purple">不可变对象</font>，list、set、dict 为<font color="purple">可变对象</font>。



## Python 数据类型转换

| 函数                                  | 说明                                     |
| ------------------------------------- | ---------------------------------------- |
| boo(obj)                              | 将 obj 转换为一个布尔值                  |
| int(obj)                              | 将 obj 转换为一个整数                    |
| float(obj)                            | 将 obj 转换为一个浮点数                  |
| complex()                             | 创建一个复数                             |
| str(obj)                              | 将 obj 转换为字符串                      |
| tuple(seq)                            | 将序列 seq 转换为一个元组                |
| list(seq)                             | 将序列 seq 转换为一个列表                |
| set(seq)                              | 将序列 seq 转换为一个集合（可变）        |
| frozenset(seq)                        | 将序列 seq 转换为一个集合（不可变）      |
| dict()                                | 创建一个字典                             |
| chr()                                 | 将一个整数转换为一个字符（Unicode 编码） |
| ord()                                 | 将一个字符转换为一个整数（Unicode 编码） |
| oct()                                 | 将一个整数转换为八进制字符串             |
| hex()                                 | 将一个整数转换为十六进制字符串           |
| <font color="purple">repr(obj)</font> | 将对象转换为表达式字符串                 |
| <font color="purple">eval()</font>    | 解析表达式字符串，并返回一个对象         |