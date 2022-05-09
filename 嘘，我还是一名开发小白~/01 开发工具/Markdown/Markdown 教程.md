<!-- @author: Zhang Jinbao -->

<!-- @date: 2021-10-22 13:16:30 -->

[TOC]

---

## Markdown 简介

```markdown
- 名称：Markdown
- 别名：MD
- 特点：轻量化、跨平台、易读易写
- 文件后缀名：`.md`、`.markdown`
- 开发者：John Gruber
```



## Markdown 是什么？

Markdown 是一种用于编写结构化文档的纯文本数据格式，由[ John Gruber ](https://daringfireball.net/projects/markdown/)于 2004 年创建，是当今世界上最受欢迎的工具之一。

- **易读易写**
- **纯文本**
- **语法简单**



## 为什么要用 Markdown？

- **可移植性**

  Markdown 是纯文本文件。

- **独立性**

  兼容任何操作系统。

- **未来性**

  适应未来变化。



## Markdown 工作原理

Markdown 应用程序使用 ==**Markdown 处理器**==将 Markdown 文件输出为<font color="blue"> **HTML 格式**</font>。

<div align="center">
    <img src="https://img-blog.csdnimg.cn/1e42710f8c2b4f36ae9acebfa2c27fb0.png" name="Markdown 工作原理" />
</div>


> ***💬说明：*** *Markdown 应用程序和 Markdown 处理器是两个不同的组件。*



## Markdown 有什么卵用？

### 网站

Markdown 最初是为 Web 而设计的。

如果你需要将 Markdown 文件进行转换为网站，可以试试以下工具：

- [Jekyll](http://jekyllcn.com/)：Markdown 网站生成器👍🏻👍🏻👍🏻
- [Read the Docs](https://readthedocs.org/)：Markdown 网站生成器
- [MkDocs](https://www.mkdocs.org/)：静态网站生成器，专门用于构建项目文档，支持 YAML
- [Docusaurus](https://www.docusaurus.cn/)：静态网站生成器，专门用于创建文档网站，支持翻译、搜索和版本控制
- [VuePress](https://vuepress.vuejs.org/)：基于 Vue 构建的静态网站生成器
- [Jetpack 插件](https://jetpack.com/)：专门用于 WordPress

> ***💬说明：*** *由于[ GitHub Pages ](https://pages.github.com/)就是基于 Jekyll 构建的，所以使用 Jekyll 就能在 GitHub 上轻而易举地免费发布网站——[自定义域名](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)等。*



### 笔记

在几乎所有方面，Markdown 都是记笔记的理想语法。

> ***💬说明：*** *目前[ Everynote ](https://www.yinxiang.com/)和[ OneNote ](https://www.onenote.com//)均不支持 Markdown，个人推荐使用[语雀](https://www.yuque.com/)👍🏻。*



### 文档

Markdown 非常适合编写技术文档。

可以使用 Markdown 文档创作工具创建 Markdown文件，并将其导出为 PDF 、或 HTML 、或其他格式。



### 书籍

想要自行出版小说？建议试试[ Leanpub](https://leanpub.com/)，它可以将你的 Markdown 文件转换为 PDF/EPUB/MOBI 格式的电子书。

如果想出版纸质书籍，可以将 PDF 文件上传到类似[ Kindle Direct Publishing ](https://kdp.amazon.com/en_US/)的服务提供商，给💰它们会帮你进行出版。



### 演示文稿

Markdown 文件可以转换成演示文稿（即：PPT）。

目前主流的 Markdown 幻灯片工具有：

- [Remarkjs](https://remarkjs.com/)
- [Cleaver](https://jdan.github.io/cleaver/)
- [Deckset](https://www.deckset.com/)
- [Marked2](https://marked2app.com/)



### 邮件

如果你需要发送大量的电子邮件，并且已经对大多数网站提供的邮件格式控件或模版感觉厌倦，可以使用 Markdown 编写电子邮件，[ Markdown Here ](https://markdown-here.com/)会助你打开新世界的大门。



## 谁在用 Markdown？

### 社区平台

- [StackOverflow](https://stackoverflow.com/)
- [CSDN](https://www.csdn.net/)
- [GitBook](https://www.gitbook.com)
- [有道云笔记](https://note.youdao.com/)
- [简书](https://www.jianshu.com/)
- [V2EX](https://www.v2ex.com/)
- [光谷社区](https://www.guozaoke.com/)
- ...



### 代码托管平台

- [GitHub](https://github.com/)
- [GitLab](https://about.gitlab.com/)
- [Gitee](https://gitee.com/)
- [BitBucket](https://bitbucket.org/)
- [Coding](https://coding.net/)
- ...



### 开源项目

- README
- 开发文档
- 帮助文档
- Wiki
- ...



## 什么是 Markdown 方言？

由于每个 Markdown 应用程序都会实现稍有不同的 Markdown 语言，这些变体通常称之为 ***flavors（方言）***。

所以作为 Markdown 的新手，我的建议是先选择一个基础 Markdown 应用程序，这对于学习 Markdown 基础语法很有帮助。



## Markdown 基本语法

### 分割线

```markdown
---

***

- - -

* * *

-----

******
```



### 标题

```perl
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/44e5d886c4cf4387bcfda0dea60eadef.png" />
</div>



### 字体

```perl
*斜体文本*
_斜体文本_

**粗体文本**
__粗体文本__

***粗斜体文本***
___粗斜体文本___

**_粗斜体文本_**
__*粗斜体文本*__
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/ab61c6924ffe441095c3e57f754351bc.gif" />
</div>



### 删除线

```markdown
~~删除文本~~
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/92943b36c79542f897933502094c4e2b.png" />
</div>


### 脚注

```markdown
[^脚注]
[^脚注]: 脚注说明。
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/b490266b381b4e4db7209b068580db31.png" />
</div>


### 无序列表

```markdown
- 第一项
- 第二项
- 第三项

* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/f74953f9fd6b4d5fb8b1cf8cfde56575.png" />
</div>



### 有序列表

```markdown
1. 第一项
2. 第二项
3. 第三项
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/c6848258c21d481dae9b84ce4038c2b0.png" />
</div>



### 引用

```perl
> 引用你所需要强调的文字
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/ae4e536698b84c09a1249aab9ec39629.png" />
</div>



### 行内代码

```markdown
`print()`
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/9d25d7aab57f4e67981db33cb93f4d21.png" />
</div>



### 代码块

````markdown
```python
插入你的代码块
```
````

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/c9c0a408d02543bbabd893c9ae26a891.png" />
</div>


### 超链接

```perl
[链接名](URL)

<URL>
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/3302d304d87b4b2b9b255d4398a403bd.png" />
</div>



### 图片

```perl
![图片名](URL)

![图片名](URL "标题")
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/3302d304d87b4b2b9b255d4398a403bd.png" />
</div>
- 图片居中

```markdown
<div align="center">
    <img src="URL" />
</div>
```

<div align="center">
    <img src="https://img-blog.csdnimg.cn/9d25d7aab57f4e67981db33cb93f4d21.png" />
</div>



### 表格

```markdown
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/bd4e8d00a00d457c9713c6ea35934bf5.png" />
</div>
- 自定义列宽

```markdown
|  <span style="display:inline-block;width: 400px">表头</span>   | <span style="display:inline-block;width: 200px">表头</span>  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

<div align="center">
    <img src="https://img-blog.csdnimg.cn/d1db54ab2638423ea7ee610e14e314a6.png" />
</div>



### 公式

```mark
$公式$

$$
公式块
$$
```

- 举个栗子🌰

<div align="center">
    <img src="https://img-blog.csdnimg.cn/f656d828ae504e699bc5d0957ad3fe53.png" />
</div>



### HTML 元素

- 粗体

  ```html
  <b>粗体文本</b>
  
  <strong>粗体文本</strong>
  ```

- 斜体

  ```html
  <i>斜体文本</i>
  
  <em>斜体文本</em>
  ```

- 下划线

  ```html
  <u>下划线文本</u>
  ```

- 上标

  ```html
  <sup>上标</sup>
  ```

- 下标

  ```html
  <sub>下标</sub>
  ```

- 字体

  ```html
  <font color="颜色">文本</font>
  ```

- 图片

  ```html
  <img src="URL" />
  ```

- 超链接

  ```html
  <a href="URL">超链接</a>
  ```

- 行内代码

  ```html
  <code>print()</code>
  ```

- 键盘文本（HTML5 已废弃）

  ```html
  <kbd>键盘文本</kbd>
  ```

- 变量

  ```html
  <var>变量</var>
  ```
  
- 换行

  ```html
  <br />
  ```

- …

