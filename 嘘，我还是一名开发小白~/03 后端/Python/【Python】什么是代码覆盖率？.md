<!-- @title: 【Python】什么是代码覆盖率？ -->
<!-- @date: 2021-10-22 13:16:30 -->
<!-- @author: Zhang Jinbao -->

[TOC]

## 何为代码覆盖率（Code Coverage）？

- 代码覆盖率可以用来发现没有被测试覆盖的代码
- 代码覆盖率不能完全用于衡量代码质量



### 做代码覆盖率有什么意义？

1. 了解测试情况，评估项目风险
2. 发现测试死角、冗余代码、废代码
3. 度量自动化用例——分析代码覆盖率，反向完善用例
4. 精准测试——构建代码调用关系，精准定位测试范围，减少资源投入



## 如何做代码覆盖率？

### 语句覆盖（Statement Coverage）

语句覆盖又称为*行覆盖（LineCoverage）、段覆盖（SegmentCoverage）、基本块覆（BasicBlockCoverage）*。

语句覆盖被称为<font color="blue">`最弱覆盖`</font>，难以发现复杂问题。

度量被测代码中<font color="purple">每个可执行语句</font>是否被执行到，不包括：头文件声明（C）、代码注释、空行等，如：

```python
def add（a, b）:  # 语句一
    # 这里是注释
    if a < 1 or b > 1:  # 语句二
        return 0  # 语句三
    else:  # 语句四
        return 1  # 语句五
```



### 判定覆盖（DecisionCoverage）

判定覆盖又称为*分支覆盖（BranchCoverage）、所有边界覆盖（All-EdgesCoverage）、基本路径覆盖（BasicPathCoverage）、判定路径覆盖（Decision-Decision-Path）*。

度量被测代码中<font color="purple">每个可判定分支</font>是否被执行到，如：

```python
def add（a, b）:
    if a < 1 or b > 1:
        return 0  # 分支一
    else:
        return 1  # 分支二
```



### 条件覆盖（ConditionCoverage）

度量判定覆盖中<font color="purple">每个子表达式结果（True/False）</font>是否被执行到，如：

```python
def add（a, b）:
    if a < 1 or b > 1:  # 子表达式
        return 0
    else:
        return 1
```

判定覆盖覆盖<font color="purple">分支</font>，条件覆盖覆盖<font color="purple">表达式</font>。

> 💬说明</font>：条件覆盖要求测试到每个子表达式的结果为 True 和 False 即可，未要求测试到每个条件表达式的结果（True, False）的排列组合。



### 路径覆盖（PathCoverage）

判定覆盖又称为断言覆盖（PredicateCoverage）。

路径覆盖被称为<font color="blue">`最强覆盖`</font>。

度量被测代码中<font color="purple">函数的每个分支</font>是否被执行到，如：

```python
def add（a, b）:
    # A 分支
    if a < 1:  # 判定
        b += 1  # A.分支一
    else:
        b += 2  # A.分支二
    # B 分支
    if b < 1:  # 判定
        return 3  # B.分支一
    else:
        return 4  # B.分支一
```



### 循环覆盖（LoopCoverage）

度量被测代码中每个循环体是否被执行了零次、一次和 N 次循环。



### 函数覆盖



### 类覆盖

