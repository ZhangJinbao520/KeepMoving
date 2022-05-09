<!-- @author: Zhang Jinbao -->

<!-- @date: 2022-01-24 13:49:18 -->

[TOC]

---

## Django 应用场景

- 网站
- 微信公众号
- 小程序

- 第三方平台
- …



## 如何创建 Django 项目？

- django-admin 已加入系统环境变量

```shell
django-admin startproject 项目名
```



## 如何启动 Django（开发模式）？

### 启动服务

```shell
python3 manage.py runserver [port]
```

### 关闭服务

- **`Ctrl`+`C`**

- **杀进程**

  - 查进程 PID

    ```shell
    lsof -i:port
    ```

  - 杀进程 PID

    ```shell
    kill -9 PID
    ```




## Django 项目结构

- **`db.sqlite3`**

  默认数据库。

- **`manage.py`**

  包含项目管理的命令。

- **项目同名文件夹**

  - **`__init__.py`**

    python 包的初始化文件。

  - **`asgi.py`**

    WEB 服务网关配置文件（异步模式）。

    > **💬说明**：`asgi.py`属于 Django 3 新增功能。

  - **`settings.py`**

    项目配置文件，包括但限不限：项目启动时所需的配置。

  - **`wsgi.py`**

    WEB 服务网关配置文件（同步模式）。

  - **`urls.py`**

    主路由配置文件。


### settings.py

`settings.py`包含了 Django 项目启动的所有配置项，主要有：

- **BASE_DIR**：项目绝对路径
- **DEBUG**：启动模式
  - **True**：调试模式
    1. 检测代码改动，立刻重启服务；
    2. 报错日志。
  - **False**：生产模式
- **ALLOWED_HOSTS**：请求 Host 头部的白名单（过滤无用的 HTTP 请求）
  - **[]**：空列表，只有请求头 Host=127.0.0.1 才允许访问
  - **[‘IP’]**：指定请求头 Host 能访问
  - **[‘*’]**：任意请求头 Host 能访问
- **ROOT_URLCONF**：指定主 URL 配置
- **LANGUAGE_CODE**：指定当前服务器语言
  - **zh-Hans**：中文
  - **en-us**：英文
  - **…**
- **TIME_ZONE**：指定当前服务器时区
  - **世界标准时间**：UTC
  - 中国时区：Asia/Shanghai
  - …
- **INSTALLED_APPS**：指定当前项目已安装的应用列表
- **MIDDLEWARE**：指定已注册的中间件
- **TEMPLATES**：指定模版的配置信息
- **DATABASES**：指定数据库的配置信息



## Django APP

- **APP 同名文件夹**

  - **`__init__.py`**

  - **`admin.py`**

    admin 后台管理（Django 提供）。

  - **`apps.py`**

    APP 启动的类。

  - **`migrations`**

    数据库变更记录（自动生成）。

    - **`__init__.py`**

  - **`models.py`**

    数据库操作。

  - **`tests.py`**

    单元测试。

  - **`views.py`**

    视图函数。

