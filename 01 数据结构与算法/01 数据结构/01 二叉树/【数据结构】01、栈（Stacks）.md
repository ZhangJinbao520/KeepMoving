<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-04-25 10:53:45 -->

[TOC]

---

## 栈

栈是一种<font color="red">**先进后出、后进先出**</font>的数据结构。

<div align="center">
    <img src="http://upload-images.jianshu.io/upload_images/10135394-ba265ee16ec5e51c.png" />
</div>



## 入栈

<div align="center">
    <img src="http://upload-images.jianshu.io/upload_images/10135394-3844f6687aea04cc.gif" />
</div>





## 出栈

<div align="center">
    <img src="http://upload-images.jianshu.io/upload_images/10135394-b8191bdd398a6634.gif" />
</div>



## 举个栗子🌰

- **题目描述**

  输入一个字符串，左右相邻的两个相同字母可以互相抵消，当抵消足够多次后，字符串的最终形态是什么？

- **示例 1**

> 输入：acbbc
>
> 输出：a

- **示例 2**

> 输入：abc
>
> 输出：abc

- **代码**

  借助栈的入栈和出栈特点

```python
s = input()
stack = []

for i in s:
    if stack:
        if stack[-1] == "(" and i == ")" or stack[-1] == "/" and i == "\\":
            # 出栈
            stack.pop()
            continue
    # 入栈 stack.push()
    stack.append(i)

print("".join(stack))
```

