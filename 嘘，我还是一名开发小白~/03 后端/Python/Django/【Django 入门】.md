组件

- 基本配置文件/路由系统

- 模型层（M）/模版层（T）/视图层（V）

  数据、CSS、submit

- Cookies 和 Session

- 分页及发邮件

- Admin 管理后台















#### 日志信息

时间、方法、协议、状态、大小



#### 启动报错

- **Error: You don't have permission to access that port.**

没权限

- **Error: That port is already in use.**

端口已被使用

被其他进程占用了





## settings.py

引入方式

```python
from django.conf import settings
```







## URL 和视图函数

### URL

统一资源定位符

uniform resource locator

作用：用来标识互联网某个资源的地址

语法格式：

```shell
protocol:// hostname[:port] / path [?query][#fragment]
```

如：http://www.baidu.com

- **protocol**：协议

  - HTTP
  - HTTPS
  - FTP
  - …

- hostname：主机名

  ​	存放资源的服务器的域名系统主机名、域名、IP 地址等

- port：端口号

- path：路由地址（更具象的资源）

  由零个或多个“/”符号隔开的字符串，一般用来表示主机上的一个目录或文件的地址

  路由地址决定服务器端如何处理这个请求

- query：查询字符串

  用于给动态网页传递参数，可有多个参数；用“&”符号隔开，每个参数的名和值用“=”符号隔开

- fragment：信息片段（锚点）

  用于指定网络资源中的片段。

  如：一个网页中有多个名词解释，可以使用 fragment 直接定位到某一个名词解释



### Django 如何处理 URL 请求？

http://127.0.0.1:8000/page/2022

- Django 从配置文件中，根据 ROOT_IRLCONF 找到主路由文件；

  默认情况下，该文件在项目同名目录下的 urls.py

- Django 加载主路由文件中的 urlpatterns 变量（包含很多路由的数组）

- 依次匹配 urlpatterns 的 path（匹配到第一个合适的中断匹配）

  - 匹配成功，调用对应的视图函数处理请求，返回响应
  - 匹配失败，返回 404

```python
# urls.py 示例
from django.urls import path
from . import views
urlpatterns = [
  path('admin/',admin.site.urls),
  path('page/2022/',views.page_2022),
  path('page/2023/',views.page_2023),
]
```





### 视图函数

用于接收一个浏览器请求（HttpRequest）

并通过 HttpResponse 对象返回响应的函数

此函数可以接收浏览器请求并根据业务落返回响应的响应内容给浏览器

```python
# 视图函数
def xxx_view(request[, 其他参数...]):
  return HttpResponse
```



## 路由配置

### path 函数

```python
def _path(route, view, kwargs=None, name=None, Pattern=None):
    if isinstance(view, (list, tuple)):
        # For include(...) processing.
        pattern = Pattern(route, is_endpoint=False)
        urlconf_module, app_name, namespace = view
        return URLResolver(
            pattern,
            urlconf_module,
            kwargs,
            app_name=app_name,
            namespace=namespace,
        )
    elif callable(view):
        pattern = Pattern(route, name=name, is_endpoint=True)
        return URLPattern(pattern, view, kwargs, name)
    else:
        raise TypeError('view must be a callable or a list/tuple in the case of include().')
```

- Route：字符串类型，匹配的请求路径
- views：指定路径所对应的视图处理函数的名称
- name：别名，在模板中地址反向解析时使用



### Path 转换器

```python
path('page/<int:page>', views.xxx)
```



语法：

```python
<转换器类型:自定义名>
```



若转换器类型匹配到对应类型的数据，则将数据按照关键字传参的方式传递给视图函数



#### 转换器类型

- **str**

  匹配除了‘/’之外的非空字符串

- **int**

  匹配 0 或任何正整数，返回一个 int

- slug

  匹配任意由 ASCII 字母或数字以及连字符和下划线组成的短标签

  ```python
  <slug:sl>
  this-is_page
  ```

- path

  匹配非空字符串，包括路径分隔符‘/’



### re_path

re_path()函数

在 URL 的匹配过程中，可以使用正则表达式精确匹配

语法：

```python
re_path(reg, view，name)
```



正则表达式为命名分组模式（`?P<name>pattern`）

匹配提取参数后，用关键字传参方式传递给视图函数







