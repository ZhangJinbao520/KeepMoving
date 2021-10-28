<!-- title: 【Python】如何做代码静态分析？ -->
<!-- date: 2021-10-24 21:59:52 -->
<!-- Table of Content -->

[TOC]

## 静态分析简介

```markdown
- 中文名：程序静态分析
- 外文名：Program Static Analysis
- 目的：规范编码规则、提升代码质量
- 特点：不实际执行程序
```



## 什么是静态分析？

静态分析是指<font color="purple">**不运行代码的情况下**</font>，通过**词法分析、语法分析、控制流分析、数据流分析**等技术对代码进行扫描，验证代码是否满足**规范性、安全性、可靠性、可维护性**等指标的一种代码分析技术。

通过静态分析可检出出以下问题，包括但不限于：**变量未定义、类型不匹配、变量操作域问题、数组下标越界、内存泄露、死锁、空指针、缓冲区溢出、安全漏斗**等问题。

> 目前全世界最好的代码分析工具误报率在 5~10%之间，能够爆出的缺陷种类也仅有几百种。



## 为什么要做代码静态分析？

在一篇名为[《 The Shift-Left Approach to Software Testing 》](https://www.cmcrossroads.com/article/shift-left-approach-software-testing)的文章中提及以下观点：

### Bug 引入

绝大多数 Bug 在编码阶段引入的。

<div align="center">
<img src="https://img-blog.csdnimg.cn/c443be09553240d5baf2b70ae1083348.png" name="软件开发的每个阶段将错误引入软件的时间" />
</div>


### Bug 发现

绝大多数 Bug 在编码阶段之后发现的。

<div align="center">
<img src="https://img-blog.csdnimg.cn/072f1f4f39ce46a79330eb1479c7d77e.png" />
</div>



### Bug 修复成本

假设在编码阶段发现缺陷只需 1 分钟修复，那么单元测试阶段需要 4 分钟、功能测试阶段需要 10 分钟、系统测试阶段需要 40 分钟、而发布之后可能需要 640 分钟。

<div align="center">
<img src="https://img-blog.csdnimg.cn/2e5e3018903944e88aac065567dfb91a.png" />
</div>



### 测试左移

静态分析也称<font color="purple">静态测试</font>，是质量内建举措中测试左移的实践之一，在静态分析阶段即可发现缺陷问题的修复成本是很低的。

<div align="center">
<img src="https://img-blog.csdnimg.cn/e8e3ca5d86d547f581c8b0e976613cd7.png" />
</div>

> “缺陷发现得越早，修复的成本越低。”——戴明曾



## 静态分析特点

- 不实际执行程序

  静态分析不运行代码，只是通过对代码的静态扫描，从而对程序进行分析。

  > <font color="purple">动态分析</font>是通过模拟环境或真实环境中执行程序进行分析的方法，多用于[性能测试](https://baike.baidu.com/item/性能测试)、[功能测试](https://baike.baidu.com/item/功能测试)、[内存泄漏](https://baike.baidu.com/item/内存泄漏)。

- 执行速率快、效率高

  成熟的静态分析工具每秒可扫描上万行代码。

- 误报率较高

  静态分析是通过对程序扫描找到匹配某种规则模式的代码，从而发现代码中存在的问题，所以有时会造成将一些正确代码识别为缺陷的问题。



## 常用的静态分析技术

- [词法分析](https://baike.baidu.com/item/词法分析)
- [语法分析](https://baike.baidu.com/item/语法分析)
- [语义分析](https://baike.baidu.com/item/语义分析)
- [抽象语法树分析](https://baike.baidu.com/item/抽象语法树)
- [控制流分析](https://baike.baidu.com/item/控制流)
- 数据流分析
- 污点分析
- 无效代码分析