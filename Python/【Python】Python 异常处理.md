<!-- title: 【Python】Python 异常处理 -->
<!-- date: 2021-10-29 11:06:25 -->
<!-- Table of Content -->

[TOC]

## 什么是异常？

异常即一个事件，该事件会在程序执行过程中发生，中断程序运行；一般情况下，当 Python 无法正常处理程序时，就会抛出一个异常。

当运行可能会出错的代码时，需要适当地添加异常处理程序，以便于阻止潜在的错误发生。

> 💬**注意**：异常也是 Python 对象，表示一个错误事件。



## Python 异常处理

捕获异常可以使用`try/except`语句。

捕获异常原理：检测 `try` 代码块中的错误，让 `except` 代码块捕获异常信息并处理。

> 💬**注意**：`try` 代码块有且仅有一个，但 `except` 代码块可以有多个且每个 `except` 代码块可同时处理多种异常



## 如何获取异常的相关信息？

在 Python 中，每个异常也是一个对象，可使用如何下方法获取当前异常的相关信息：

- <font color="purple">**e.args**</font>：返回异常信息的错误编号和描述字符串
- <font color="purple">**str(e)**</font>：返回异常信息，但不包括异常信息的类型
- <font color="purple">**repr(e)**</font>：返回较全的异常信息，包括异常信息的类型

```python
>>> try:
...     a = 1/0
... except Exception as e:
...     print(e.args)
...     print(str(e))
...     print(repr(e))
('division by zero',)
division by zero
ZeroDivisionError('division by zero')
```



## try … excepet …

```python
try:
    可能产生异常的代码块
except [ (Error1, Error2, ... ) [as e] ]:
    处理异常的代码块
except  [Exception]:
    处理其它异常的代码块
```

### 举个栗子🌰

```python
>>> try:
...     a = 1/0
... except ZeroDivisionError as e:
...     print("被除数不能为 0 ")
... except Exception as e:
...     print("其他异常")
被除数不能为 0 
```



## try … excepet … else …

```python
try:
    可能产生异常的代码块
except [ (Error1, Error2, ... ) [as e] ]:
    处理异常的代码块
except  [Exception]:
    处理其它异常的代码块
else:
    未发生异常的代码块
```

> 💬**注意**：当 `try` 代码块有 return 代码时，不会执行 `else` 代码块。

### 举个栗子🌰

```python
>>> try:
...     a = 1/1
... except ZeroDivisionError as e:
...     print("被除数不能为 0 ")
... except Exception as e:
...     print("其他异常")
... else:
... 		print("没有异常")
没有异常
```



## try … finally …

```python
try:
    可能产生异常的代码块
finally:
  	最后一定会执行的代码块
```

> 💬**注意**：不管 `try` 代码块是否有 return 代码时，都会执行 `finally` 代码块。

### 举个栗子🌰

```python
>>> try:
...     a = 1/1
... finally:
...     print("finally")
finally
```



## try … excepet … finally …

```python
try:
    可能产生异常的代码块
except [ (Error1, Error2, ... ) [as e] ]:
    处理异常的代码块
except  [Exception]:
    处理其它异常的代码块
finally:
  	最后一定会执行的代码块
```

### 举个栗子🌰

```python
>>> try:
...     a = 1/1
... except ZeroDivisionError as e:
...     print("被除数不能为 0 ")
... except Exception as e:
...     print("其他异常")
... finally:
...     print("finally")
finally
```



## try … excepet … else … finally …

```python
try:
    可能产生异常的代码块
except [ (Error1, Error2, ... ) [as e] ]:
    处理异常的代码块
except  [Exception]:
    处理其它异常的代码块
else:
    未发生异常的代码块
finally:
  	最后一定会执行的代码块
```

### 举个栗子🌰

```python
>>> try:
...     a = 1/1
... except ZeroDivisionError as e:
...     print("被除数不能为 0 ")
... except Exception as e:
...     print("其他异常")
... else:
... 		print("没有异常")
... finally:
...     print("finally")
没有异常
finally
```



---

## 附录：Python 标准异常

| 异常名称                                     | 异常说明                                           | 适用版本   |
| -------------------------------------------- | -------------------------------------------------- | ---------- |
| BaseException                                | 所有异常的基类                                     | ALL        |
| <font color="red">Exception</font>           | 所有常规异常的基类                                 | ALL        |
| StopIteration                                | 迭代器没有更多的值                                 | ALL        |
| GeneratorExit                                | 生成器异常退出（Generator）                        | ALL        |
| SystemExit                                   | Python 解释器异常退出                              | ALL        |
| StandardError                                | 所有内建标准异常的基类                             | Python 2.x |
| ArithmeticError                              | 所有数值计算异常的基类                             | ALL        |
| ZeroDivisionError                            | （整）除零错误                                     | ALL        |
| FloatingPointError                           | 浮点数计算异常                                     | ALL        |
| OverflowError                                | 数值超出最大限制                                   | ALL        |
| AssertionError                               | 断言异常                                           | ALL        |
| <font color="red">AttributeError</font>      | 对象没有该属性                                     | ALL        |
| <font color="red">EOFError</font>            | 没有内建输入，到达EOF 标记                         | ALL        |
| EnvironmentError                             | 所有操作系统异常的基类                             | ALL        |
| IOError                                      | 输入/输出异常                                      | ALL        |
| OSError                                      | 操作系统异常                                       | ALL        |
| WindowsError                                 | 系统调用异常                                       | Python 2.x |
| <font color="red">ImportError</font>         | 导入模块/对象异常                                  | ALL        |
| KeyboardInterrupt                            | 用户中断执行（`Ctrl`+`C`）                         | ALL        |
| LookupError                                  | 所有无效查询异常的基类                             | ALL        |
| <font color="red">IndexError</font>          | 序列中索引异常（Index）                            | ALL        |
| <font color="red">KeyError</font>            | 映射中键异常（Key）                                | ALL        |
| MemoryError                                  | 内存溢出异常                                       | ALL        |
| <font color="red">NameError</font>           | 未声明/初始化对象（没有属性）                      | ALL        |
| UnboundLocalError                            | 访问未初始化的本地变量                             | ALL        |
| ReferenceError                               | 试图访问已垃圾回收的对象——弱引用（Weak reference） | ALL        |
| RuntimeError                                 | 一般运行的异常                                     | ALL        |
| <font color="red">NotImplementedError</font> | 尚未实现的方法                                     | ALL        |
| <font color="red">SyntaxError</font>         | 语法异常                                           | ALL        |
| IndentationError                             | 缩进异常                                           | ALL        |
| TabError                                     | tab 和空格混用异常                                 | ALL        |
| SystemError                                  | 解释器系统异常                                     | ALL        |
| SystemExit                                   | 解释器请求退出                                     | ALL        |
| TypeError                                    | 类型异常（对类型无效操作）                         | ALL        |
| <font color="red">ValueError</font>          | 值异常（传入无效参数）                             | ALL        |
| UnicodeError                                 | 所有 Unicode 异常的基类                            | ALL        |
| UnicodeDecodeError                           | Unicode 解码异常                                   | ALL        |
| UnicodeEncodeError                           | Unicode 编码异常                                   | ALL        |
| UnicodeTranslateError                        | Unicode 转换异常                                   | ALL        |
| Warning                                      | 所有警告异常的基类                                 | ALL        |
| DeprecationWarning                           | 被弃用特征的警告                                   | ALL        |
| FutureWarning                                | 构造将来语义改变的警告                             | ALL        |
| OverflowWarning                              | 自动转为长整型的警告                               | Python 2.x |
| PendingDeprecationWarning                    | 关于特性将会被废弃的警告                           | ALL        |
| RuntimeWarning                               | 可疑的运行警告                                     | ALL        |
| SyntaxWarning                                | 可疑的语法警告                                     | ALL        |
| UserWarning                                  | 用户代码生成的警告                                 | ALL        |







