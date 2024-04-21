---
icon: material/format-align-bottom
---

# 脚注 Footnotes {#footnotes}

脚注是一种在不中断文档流的情况下，为特定单词、短语或句子添加补充信息或附加信息的绝佳方式。Material for MkDocs 提供了定义、引用和渲染脚注的功能。

## 配置 {#configuration}

此配置增加了定义内联脚注的能力，这些脚注随后将在文档的所有 Markdown 内容下方渲染。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - footnotes
```

查看其他配置选项：

- [脚注]

  [脚注]: ../setup/extensions/python-markdown.md#footnotes

### 脚注工具提示 :material-alert-decagram:{ .mdx-pulse title="2024年1月24日添加" } {#footnote-tooltips}

<!-- md:sponsors -->
<!-- md:version insiders-4.51.0 -->
<!-- md:flag experimental -->

[Insiders] 允许将脚注渲染为内联工具提示，因此用户可以在不离开文档上下文的情况下阅读脚注。脚注工具提示可以在 `mkdocs.yml` 中启用：

``` yaml
theme:
  features:
    - content.footnote.tooltips
```

__在我们的文档中启用了脚注工具提示__，因此要尝试它，您可以在本页面或我们文档的任何其他页面上悬停或聚焦任何脚注。

  [Insiders]: ../insiders/index.md

## 用法 {#usage}

### 添加脚注引用 {#adding-footnote-references}

脚注引用必须用方括号括起来，并且必须以插入符号 `^` 开头，紧接着是一个任意标识符，类似于标准 Markdown 链接语法。

``` title="Text with footnote references"
Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]
```

<div class="result" markdown>

Lorem ipsum[^1] dolor sit amet, consectetur adipiscing elit.[^2]

</div>

### 添加脚注内容 {#adding-footnote-content}

脚注内容必须使用与引用相同的标识符声明。它可以在文档中的任意位置插入，并且总是在页面底部渲染。此外，自动添加回到脚注引用的反向链接。

#### 单行上 {#on-a-single-line}

短脚注可以在同一行上编写：

``` title="Footnote"
[^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

<div class="result" markdown>

[:octicons-arrow-down-24: Jump to footnote](#fn:1)

</div>

  [^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.

#### 多行上 {#on-multiple-lines}

段落可以在下一行编写，并且必须缩进四个空格：

``` title="Footnote"
[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

<div class="result" markdown>

[:octicons-arrow-down-24: Jump to footnote](#fn:2)

</div>

[^2]:
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus
    auctor massa, nec semper lorem quam in massa.
