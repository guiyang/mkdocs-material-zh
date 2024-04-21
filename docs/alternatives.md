# 替代方案 {#alternatives}

市面上有许多静态网站生成器和主题，选择适合您技术栈的正确方案是一个艰难的决定。如果您不确定 Material for MkDocs 是否适合您，本节应该可以帮助您评估其他解决方案。

## Docusaurus

由 Facebook 开发的 [Docusaurus] 是一个非常受欢迎的文档生成器，如果您或您的公司已经在使用 [React] 构建网站，它是一个不错的选择。它将生成一个[单页应用程序]，这与 Material for MkDocs 为您生成的站点在根本上不同。

__优势__

- 非常强大，可定制性和扩展性强
- 提供许多有助于技术写作的组件
- 拥有大型且丰富的生态系统，由 Facebook 支持

__挑战__

- 学习曲线较高，需要掌握 JavaScript
- JavaScript 生态系统非常不稳定，维护成本较高
- 需要更多时间才能开始使用

虽然 [Docusaurus] 是一个在生成单页应用程序方面表现出色的文档站点的最佳选择之一，但还有许多其他解决方案，包括 [Docz]、[Gatsby]、[Vuepress] 和 [Docsify]，这些解决方案以类似的方式处理这个问题。

  [Docusaurus]: https://docusaurus.io/
  [React]: https://reactjs.org/
  [单页应用程序]: https://en.wikipedia.org/wiki/Single-page_application
  [Docz]: https://www.docz.site/
  [Gatsby]: https://www.gatsbyjs.com/
  [VuePress]: https://vuepress.vuejs.org/
  [Docsify]: https://docsify.js.org/

## Jekyll

[Jekyll] 可能是最成熟和广泛使用的静态站点生成器之一，它使用 [Ruby] 编写。它不是专门针对技术项目文档的，并且有许多可供选择的主题，这可能是一个挑战。

__优势__

- 经过实战测试，生态系统丰富，可选择多种主题
- 提供出色的博客功能（永久链接、标签等）
- 生成的站点对搜索引擎优化友好，类似于 Material for MkDocs

__挑战__

- 不专门针对技术项目文档
- Markdown 功能有限，不如 Python Markdown 高级
- 需要更多时间才能开始使用

  [Jekyll]: https://jekyllrb.com/
  [Ruby]: https://www.ruby-lang.org/de/

## Sphinx

[Sphinx] 是另一种静态站点生成器，专门用于生成参考文档，提供 MkDocs 缺乏的强大功能。它使用 [reStructured text]，这是一种类似于 Markdown 的格式，一些用户发现它更难使用。

__优势__

- 非常强大，可定制性和扩展性强
- 从 [Python docstrings] 生成参考文档
- 拥有大型且丰富的生态系统，许多 Python 项目都在使用

__挑战__

- 学习曲线较高，[reStructured text] 语法可能具有挑战性
- 搜索功能不如 MkDocs 提供的强大
- 需要更多时间才能开始使用

如果您正在考虑使用 Sphinx，因为您需要生成参考文档，您应该尝试 [mkdocstrings] —— 一个活跃维护且流行的框架，基于 MkDocs 实现类似 Sphinx 的功能。

  [Sphinx]: https://www.sphinx-doc.org/
  [reStructured text]: https://en.wikipedia.org/wiki/ReStructuredText
  [Python docstrings]: https://www.python.org/dev/peps/pep-0257/
  [mkdocstrings]: https://github.com/mkdocstrings/mkdocstrings

## GitBook

[GitBook] 提供一个托管的文档解决方案，可以从您的 GitHub 仓库中的 Markdown 文件生成一个美观且功能完善的站点。然而，它曾经是开源的，但一段时间前转变为封闭源代码解决方案。

__优势__

- 托管解决方案，技术知识要求最低
- 自定义域名、认证和其他企业功能
- 出色的团队协作功能

__挑战__

- 封闭源代码，专有项目不免费
- Markdown 功能有限，不如 Python Markdown 高级
- 许多开源项目已从 GitBook 转移

许多用户从 [GitBook] 转向 Material for MkDocs，因为他们希望保持对他们文档的控制和所有权，偏好一个开源解决方案。

  [GitBook]: https://www.gitbook.com/
