<!-- title: 【Markdown】Markdown 入门基础（一） -->
<!-- date: 2021-10-22 13:16:30 -->
<!-- Table of Content -->
[TOC]

## Markdown 是什么？
Markdown 是一种用于编写结构化文档的纯文本格式约定，由[ John Gruber ](https://daringfireball.net/projects/markdown/) [^1] 于 2004 年创建，是如今世界最受欢迎的工具之一。
[^1]: [Markdown 创建者编写的原始指南](https://daringfireball.net/projects/markdown/)：不再维护（上次更新于 2004 年 12 月）
- 易读易写
- 纯文本，可纳入版本控制
- 语法简单，学习成本低

## Markdown 发展史。
- John Gruber [介绍 Markdown](https://daringfireball.net/2004/03/introducing_markdown) - 2004 年 3 月 15 日
  > 我编写了一个名为 Markdown 的文本到 HTML 格式工具，现在可以下载。
- John Gruber [Dive into Markdown](https://daringfireball.net/2004/03/dive_into_markdown) - 2004 年 3 月 19 日
  > 您不需要在发送电子邮件之前“预览”它——您可以在那里编写、阅读、编辑它。
- Aaron Swartz [Markdown](http://www.aaronsw.com/weblog/001189) - 2004 年 3 月 22 日

## 为什么要用 Markdown？
- 可移植性（由于是纯文本）
- 独立性（兼容任何操作系统）
- 未来性（能适应未来变化）

## Markdown 工作原理。
默认以`.md`或`.Markdown`为扩展名的文件，均视为 Markdown 文件。  
Markdown 应用程序使用 **Markdown 处理器**将 Markdown文件输出为 **HTML 格式**。
<div align="center">
<img src="https://img-blog.csdnimg.cn/1e42710f8c2b4f36ae9acebfa2c27fb0.png" />
</div>
<!-- 部分网站必须空行，统一标准 -->

**💬注意**： Markdown 应用程序和 Markdown 处理器是两个不同的组件。

## Markdown 有什么卵用？
### 网站
Markdown 最初是为 Web 而设计的。  
如果你需要将 Markdown 文件进行转换为网站，可以试试以下工具：
- [**Jekyll**](http://jekyllcn.com/)： Markdown 网站生成器👍🏻
- [**Read the Docs**](https://readthedocs.org/)： Markdown 网站生成器
- [**MkDocs**](https://www.mkdocs.org/)：静态网站生成器，专门用于构建项目文档，支持 YAML
- [**Docusaurus**](https://www.docusaurus.cn/)：静态网站生成器，专门用于创建文档网站，支持翻译、搜索和版本控制
- [**VuePress**](https://vuepress.vuejs.org/)：基于 Vue 构建的静态网站生成器
- [**Jetpack 插件**](https://jetpack.com/)：专门用于 WordPress

> 由于[ GitHub Pages ](https://pages.github.com/)就是基于 Jekyll 构建的，所以使用 Jekyll 轻而易举地在 GitHub 上免费发布网站——[自定义域名](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)等等。

### 笔记
在几乎所有方面，Markdown 都是记笔记的理想语法。  
**💬注意**：目前[ Everynote ](https://www.yinxiang.com/)和 [ OneNote ](https://www.onenote.com//)均不支持 Markdown，个人推荐使用[语雀](https://www.yuque.com/)👍🏻。

### 文档
Markdown 非常适合编写技术文档。  
可以使用 Markdown 文档创作工具创建 Markdown文件，并将其导出为 PDF 、或 HTML 、或其他格式。

### 书籍
想要自行出版小说？建议试试[ Leanpub ](https://leanpub.com/)，它可以将你的 Markdown文件转换为 PDF/EPUB/MOBI 格式的电子书。  
如果想出版纸质书籍，可以将 PDF 文件上传到类似[ Kindle Direct Publishing ](https://kdp.amazon.com/en_US/)的服务提供商，它们会帮你进行出版💰。

### 演示文稿
Markdown 文件可以转换成演示文稿（即：PPT）。  
目前主流的 Markdown 幻灯片工具有：
- [Remarkjs](https://remarkjs.com/)
- [Cleaver](https://jdan.github.io/cleaver/)
- [Deckset](https://www.deckset.com/)
- [Marked2](https://marked2app.com/)

### 邮件
如果你需要发送大量的电子邮件，并且已经对大多数网站提供的邮件格式控件或模版感觉厌倦，可以使用 Markdown 编写电子邮件，[ Markdown Here ](https://markdown-here.com/)会助你打开新世界的大门。

## 都有谁在用 Markdown？
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
由于每个 Markdown 应用程序都会实现稍有不同的 Markdown 语言，这些变体通常称之为 *flavors（方言）*。  
所以作为 Markdown 的新手，我的建议是先选择一个基础 Markdown 应用程序，这对于学习 Markdown 基础语法很有帮助。