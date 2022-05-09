<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-03-18 15:45:31 -->

[TOC]

---

## Git 原理

1. Git 初始化
    ```
    操作
        git init
    校验
        find .
    ```
2. 创建文件
    ```
    操作
        vim xxx
    校验
        find .
        git status
    ```
3. 创建对象
    ```
    操作
        git hash-object -w xxx
    校验
        find .
        git status
    ```
4. 更新索引（暂存区）
    ```
    操作
        git update-index --add --cache 100644 SHA1xxx xxx
        git update-index xxx
    校验
        find .
        git status
    ```
5. 创建 tree 对象
    ```
    操作
        git write-tree
    校验
        find .
        git status
    ```
6. 创建 commit-tree 对象
    ```
    操作
        git commit-tree SHA1xxx
    校验
        find .
        git status
        git tree
        git log SHA1xxx
    ```
7. 打包
    ```
    操作
        git gc
    ```

