<!-- title: 【Python】Python 入门基础（二） -->
<!-- date: 2021-10-26 16:19:25 -->
<!-- Table of Content -->

[TOC]

## Python 序列

序列是一种**数据存储方式**，是一块用来存放多个值的<font color="purple">**连续内存空间**</font>，包括但不限于：*str（字符串）、tuple（元组）、list（列表）、set （集合）、dict（字典）*。

### 有序列表

有序列表包括：**str（字符串）、tuple（元组）、list（列表）**，具有以下特性：

- 支持索引访问（从 0 开始）

  > object[0]

- 支持切片

  > object==**[start: end: step]**==

  - 不可变对象
    - [::]：不产生新对象
    - \[x:y:z\]：产生新对象
  - 可变对象
    - [::]：产生新对象
    - \[x:y:z\]：产生新对象

  > 💬**注意**：原对象和切片产生的新对象，共享子对象内存。

- 支持拼接（产生新对象）

  > object + object

<div align="center">
<img src="https://img-blog.csdnimg.cn/dd6d9d18061c4d6da9aed75aea7315a4.png" name="有序列表"/>
</div>

```python
# str --索引访问
>>> var = "Hello World"
>>> print(var[0])
H

# str --切片
>>> var = "Hello World"
>>> print(var[0:2:])
He

# str --拼接
>>> var1 = "Hello "
>>> var2 = "World"
>>> print(var1 + var2)
Hello World

# tuple --索引访问
>>> var = (1, 2, 3)
>>> print(var[0])
1

# tuple --切片
>>> var = (1, 2, 3)
>>> print(var[0:2:])
(1, 2)

# tuple --拼接
>>> var1 = (1, 2)
>>> var2 = (3, )
>>> print(var1 + var2)
(1, 2, 3)

# list --索引访问
>>> var = [1, 2, 3]
>>> print(var[0])
1

# list --切片
>>> var = [1, 2, 3]
>>> print(var[0:2:])
[1, 2]

# list --拼接
>>> var1 = [1, 2]
>>> var2 = [3]
>>> print(var1 + var2)
[1, 2, 3]
```



### 无序列表

无序列表包括：**set （集合）、dict（字典）**；主要有以下特性：

- 不支持索引访问（从 0 开始）

  > TypeError: 'set' object is not subscriptable

- 不支持切片

  > TypeError: unhashable type: 'slice'

- 不支持拼接

  > TypeError: unsupported operand type(s) for +: 'set' and 'set'
  >
  > TypeError: unsupported operand type(s) for +: 'dict' and 'dict'

```python
# set --索引访问
>>> var = {1, 2}
>>> print(var[0])
TypeError: 'set' object is not subscriptable
TypeError: 'set' object does not support indexing

# set --切片
>>> var = {1, 2}
>>> print(var[0:2:])
TypeError: 'set' object is not subscriptable
TypeError: 'set' object has no attribute '__getitem__'

# set --拼接
>>> var1 = "Hello "
>>> var2 = "World"
>>> print(var1 + var2)
TypeError: unsupported operand type(s) for +: 'set' and 'set'

# dict --索引访问
>>> var = {"1": "2", "3": "4"}
>>> print(var[0])
KeyError

# dict --切片
>>> var = {"1": "2", "3": "4"}
>>> print(var[0:2:])
TypeError: unhashable type: 'slice'

# dict --拼接
>>> var1 = {"1": "2"}
>>> var2 = {"3": "4"}
>>> print(var1 + var2)
TypeError: unsupported operand type(s) for +: 'dict' and 'dict'
```



### Number（数字）

Python 支持 **int、float、bool、complex（复数）**。

> 💬**注意**：float 类型在内存中使用**科学计数法**进行存储，如：π为 314E-2（即：314*10^-2）。

> 💬**注意**：在 Python2 中，int 类型为 32 bits、long 类型为 64 bits；而在 Python3 中，取消了整数的长度限制。

> 💬**注意**：在 Python2 中，未定义 bool 类型，使用 1 表示 True、0 表示 False；而在 Python3 中，定义了 bool 类型且 **作为 int 的子类**， True/False 可以和数字直接相加。

```python
# 整数定义
>>> var = 1
>>> print(var)
1

# 浮点数定义
>>> var = 1.0
>>> print(var)
1.0

# 布尔值定义
>>> var = True
>>> print(var)
True

# 复数定义
>>> var = complex(3, 4)
>>> print(var)
(3+4j)
```



#### Number 方法

```python
# int 方法
['__repr__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__add__', '__radd__', '__sub__', '__rsub__', '__mul__', '__rmul__', '__mod__', '__rmod__', '__divmod__', '__rdivmod__', '__pow__', '__rpow__', '__neg__', '__pos__', '__abs__', '__bool__', '__invert__', '__lshift__', '__rlshift__', '__rshift__', '__rrshift__', '__and__', '__rand__', '__xor__', '__rxor__', '__or__', '__ror__', '__int__', '__float__', '__floordiv__', '__rfloordiv__', '__truediv__', '__rtruediv__', '__index__', '__new__', 'conjugate', 'bit_length', 'to_bytes', 'from_bytes', 'as_integer_ratio', '__trunc__', '__floor__', '__ceil__', '__round__', '__getnewargs__', '__format__', '__sizeof__', 'real', 'imag', 'numerator', 'denominator', '__doc__', '__str__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__dir__', '__class__']

# float 方法
['__repr__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__add__', '__radd__', '__sub__', '__rsub__', '__mul__', '__rmul__', '__mod__', '__rmod__', '__divmod__', '__rdivmod__', '__pow__', '__rpow__', '__neg__', '__pos__', '__abs__', '__bool__', '__int__', '__float__', '__floordiv__', '__rfloordiv__', '__truediv__', '__rtruediv__', '__new__', 'conjugate', '__trunc__', '__floor__', '__ceil__', '__round__', 'as_integer_ratio', 'fromhex', 'hex', 'is_integer', '__getnewargs__', '__getformat__', '__set_format__', '__format__', 'real', 'imag', '__doc__', '__str__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__sizeof__', '__dir__', '__class__']

# bool 方法
['__repr__', '__and__', '__rand__', '__xor__', '__rxor__', '__or__', '__ror__', '__new__', '__doc__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__add__', '__radd__', '__sub__', '__rsub__', '__mul__', '__rmul__', '__mod__', '__rmod__', '__divmod__', '__rdivmod__', '__pow__', '__rpow__', '__neg__', '__pos__', '__abs__', '__bool__', '__invert__', '__lshift__', '__rlshift__', '__rshift__', '__rrshift__', '__int__', '__float__', '__floordiv__', '__rfloordiv__', '__truediv__', '__rtruediv__', '__index__', 'conjugate', 'bit_length', 'to_bytes', 'from_bytes', 'as_integer_ratio', '__trunc__', '__floor__', '__ceil__', '__round__', '__getnewargs__', '__format__', '__sizeof__', 'real', 'imag', 'numerator', 'denominator', '__str__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__dir__', '__class__']

# complex 方法
['__repr__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__add__', '__radd__', '__sub__', '__rsub__', '__mul__', '__rmul__', '__mod__', '__rmod__', '__divmod__', '__rdivmod__', '__pow__', '__rpow__', '__neg__', '__pos__', '__abs__', '__bool__', '__int__', '__float__', '__floordiv__', '__rfloordiv__', '__truediv__', '__rtruediv__', '__new__', 'conjugate', '__getnewargs__', '__format__', 'real', 'imag', '__doc__', '__str__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__sizeof__', '__dir__', '__class__']
```



#### Number 特性

- **不可变对象**（不可变长度）
  - 不支持新增
  - 不支持删除
  - 不支持修改
  - 支持查询
- **非序列**
  - 不支持下标访问（从 0 开始）
  - 不支持切片

  - 不支持拼接



```python
# 不可变对象——如果需要改变原值，则需要创建新对象并赋值
>>> var = 1
>>> print(var)
1
>>> print(id(var))
140407628503344
>>> var = 2
>>> print(var)
2
>>> print(id(var))
140407628503408

# 非序列——不支持下标访问
>>> var = 1
>>> print(var[0])
TypeError: 'int' object is not subscriptable
```



### str（字符串）

字符串是写在两个单引号 ==**'**== 或双引号 ==**"**== 之间。

```python
# 字符串定义
>>> var = "Hello world"
>>> print(var)
Hello world

# 0 个元素（空字符串）
>>> var = ""
>>> var
''

# 1 个元素
>>> var = "1"
>>> print(var)
1
```



#### str 方法

```python
# str 方法
['__repr__', '__hash__', '__str__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__iter__', '__mod__', '__rmod__', '__len__', '__getitem__', '__add__', '__mul__', '__rmul__', '__contains__', '__new__', 'encode', 'replace', 'split', 'rsplit', 'join', 'capitalize', 'casefold', 'title', 'center', 'count', 'expandtabs', 'find', 'partition', 'index', 'ljust', 'lower', 'lstrip', 'rfind', 'rindex', 'rjust', 'rstrip', 'rpartition', 'splitlines', 'strip', 'swapcase', 'translate', 'upper', 'startswith', 'endswith', 'removeprefix', 'removesuffix', 'isascii', 'islower', 'isupper', 'istitle', 'isspace', 'isdecimal', 'isdigit', 'isnumeric', 'isalpha', 'isalnum', 'isidentifier', 'isprintable', 'zfill', 'format', 'format_map', '__format__', 'maketrans', '__sizeof__', '__getnewargs__', '__doc__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__dir__', '__class__']
```



#### str 特性


- **不可变对象**（不可变长度）
  - 不支持新增
  - 不支持删除
  - 不支持修改
  - 支持查询
- **有序序列**

  - 支持下标访问（从 0 开始）
  - 支持切片
  - 支持拼接

```python
# 不可变对象——如果需要改变原值，则需要创建新对象并赋值
>>> var = "Hello world"
>>> print(var)
Hello world
>>> print(id(var))
140706160398064
>>> var = "Hello world !"
>>> print(var)
Hello world !
>>> print(id(var))
140706160398192

# 有序序列——支持下标访问
>>> var = "Hello world"
>>> print(var[0])
H

# 支持切片
>>> var = "Hello world"
>>> print(var[0:])
Hello world

# 支持拼接
>>> print("Hello " + "world")
Hello world
```






- **转义字符**： \
- **原始字符串**：r

```python
# 字符转义
>>> print("Hello\nworld")
Hello
world

# 原始字符串
>>> print(r"Hello\nworld")
Hello\nworld
```

> 💬**注意**：Python 没有字符类型，1 个字符就是长度为 1 的字符串。



### tuple（元组）

元组写在小括号 ==**()**== 之间，元素用逗号 ==**,**== 分隔。

> 💬**注意**：由于 **()** 与运算方法冲突，所以当构造仅有 0 个或 1 个元素的元组时需使用特殊语法。

```python
# 元组定义
>>> var = (1, 2, "3")
>>> print(var)
(1, 2, "3")

# 0 个元素（空元组）
>>> var = ()
>>> print(var)
()

# 1 个元素——需要在元素后添加逗号
>>> var = (1,)
>>> print(var)
(1,)
```

#### tuple 方法

```python
# 元组方法
['__repr__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__iter__', '__len__', '__getitem__', '__add__', '__mul__', '__rmul__', '__contains__', '__new__', '__getnewargs__', 'index', 'count', '__class_getitem__', '__doc__', '__str__', '__setattr__', '__delattr__', '__init__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__format__', '__sizeof__', '__dir__', '__class__']
```

#### tuple 特性

- 不可变对象（不可变长度）

  - 不支持新增
  - 不支持删除
  - 不支持修改
  - 支持查询

- 序列（有序）

  - 支持切片

    > 通过下标访问元素（从 0 开始）

  - 支持拼接

  - 支持任意嵌套
  
    - 可包含任意对象

```python
# 元组切片——可切片读（有序序列）
>>> var = (1, 2)
>>> print(var[0:])
(1, 2)

# 元组拼接
>>> var = (1, 2)
>>> print(var + (3, ))
(1, 2, 3)

# 任意嵌套
>>> var = (1, "2", (3, 4), [5, 6], {7, 8}, {9: 10})
>>> print(var)
(1, "2", (3, 4), [5, 6], {7, 8}, {9: 10})


# 读元组--可切片读（序列）
>>> var = (1, 2)
>>> print(var[0:])
(1, 2)

# 写元组--不支持下标（不可变对象）
>>> var = (1, 2)
>>> var[0] = 3

TypeError: 'tuple' object does not support item assignment
```



### list（列表）

列表是写在方括号 ==**[] **== 之间，元素用逗号 ==**,**== 分隔。

- 可变对象
- 序列（有序）——可通过下标访问，从 0 开始
- 可包含任意对象
- 长度可变
- 长度可变，任意嵌套
- 支持原位改变

#### list 方法

```python
# 列表方法
['__repr__', '__hash__', '__getattribute__', '__lt__', '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__iter__', '__init__', '__len__', '__getitem__', '__setitem__', '__delitem__', '__add__', '__mul__', '__rmul__', '__contains__', '__iadd__', '__imul__', '__new__', '__reversed__', '__sizeof__', 'clear', 'copy', 'append', 'insert', 'extend', 'pop', 'remove', 'index', 'count', 'reverse', 'sort', '__class_getitem__', '__doc__', '__str__', '__setattr__', '__delattr__', '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__', '__format__', '__dir__', '__class__']
```

#### list 特性


```python
# 列表定义
>>> var = [1, 2, "3"]
>>> print(var)
[1, 2, "3"]

# 列表拼接
>>> var = [1, 2]
>>> print(var + [3])
[1, 2, 3]

# 0 个元素（空列表）
>>> var = []
>>> print(var)
[]

# 1 个元素
>>> var = [1]
>>> print(var)
[1]

# 读列表--可切片读（序列）
>>> var = [1, 2]
>>> print(var[0:])
[1, 2]

# 写列表--支持下标（可变对象）
>>> var = [1, 2]
>>> var[0] = 3
>>> print(var)
[3, 2]
```



### set（集合）

集合是写在大括号 ==**{} **== 之间，元素用逗号 ==**,**== 分隔。



- 可变对象
- 序列（无序）
- 

> 💬**注意**：<font color="purple">**集合中各元素之间都是不相同的（自动去重）**</font>。

> 💬**注意**：由于 **{}** 与创建字典方法冲突，所以当创建一个空集合时必须使用 **set()**。

#### set 方法

#### set 特性

```python
# 集合定义
>>> var = {1, 2, "3"}
>>> print(var)
{1, 2, "3"}

# 0 个元素（空集合）
>>> var = set()
>>> print(var)
[]

# 1 个元素
>>> var = {1}
>>> print(var)
{1}

# 集合运算
>>> a = {1, 2, 3}
>>> b = {1, 2, 4}
>>> print(a | b)  # a 和 b 的并集（a∪b）
{1, 2, 3, 4}
>>> print(a & b)  # a 和 b 的交集（a∩b）
{1, 2}
>>> print(a - b)  # a 和 b 的差集
{3}
>>> print(a ^ b)  # a 和 b 的不同时存在的元素集合（a∪b - a∩b）
{3, 4}

# 读集合--不可切片读（非序列）
>>> var = {1, 2}
>>> print(var[0:])

TypeError: 'set' object is not subscriptable

# 写集合--不支持下标（可变对象）
>>> var = [1, 2]
>>> var[0] = 3

TypeError: 'set' object does not support item assignment
```



### dict（字典）

字典是写在大括号 ==**{} **== 之间，元素用逗号 ==**,**== 分隔，以“**键（Key）: 值（Value）**”作为一个元素。

> 💬**注意**：键（Key）必须为==**不可变对象**==且==**唯一**==。

> 💬**注意**：列表是有序的对象集合，字典是无序的对象集合，两者之间主要区别在于：**列表通过偏移进行读写，而字典通过键进行读写**。

#### dict方法

#### dict特性

```python
# 字典定义
>>> var = {1: 2, 2: 3}
>>> print(var)
{1: 2, 2: 3}

# 0 个元素（空字典）
>>> var = {}
>>> print(var)
{}

# 1 个元素
>>> var = {1: 2}
>>> print(var)
{1: 2}

# 读字典--不可切片读（非序列）
>>> var = {1: 2}
>>> print(var[1:])

TypeError: unhashable type: 'slice'

# 写字典--支持下标（可变对象）
>>> var = {1: 2}
>>> var[1] = 3
>>> print(var)
{1: 3}
```
