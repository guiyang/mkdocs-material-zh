---
title: 扩展
---

# 扩展 {#extensions}

Markdown 是一种非常简单的语言，有一个被称为 [John Gruber's Markdown] 的类参考实现。[Python Markdown] 和 [Python Markdown Extensions] 是两个增强 Markdown 写作体验的包，为技术写作添加了有用的语法扩展。

  [John Gruber's Markdown]: https://daringfireball.net/projects/markdown/
  [Python Markdown]: python-markdown.md
  [Python Markdown Extensions]: python-markdown-extensions.md

## 支持的扩展 {#supported-extensions}

以下扩展均由 Material for MkDocs 支持，因此强烈推荐。点击每个扩展了解其用途和配置：

<div class="mdx-columns" markdown>

- [Abbreviations]
- [Admonition]
- [Arithmatex]
- [Attribute Lists]
- [BetterEm]
- [Caret, Mark & Tilde]
- [Critic]
- [Definition Lists]
- [Details]
- [Emoji]
- [Footnotes]
- [Highlight]
- [Keys]
- [Markdown in HTML]
- [SmartSymbols]
- [Snippets]
- [SuperFences]
- [Tabbed]
- [Table of Contents]
- [Tables]
- [Tasklist]

</div>

  [Abbreviations]: python-markdown.md#abbreviations
  [Admonition]: python-markdown.md#admonition
  [Arithmatex]: python-markdown-extensions.md#arithmatex
  [Attribute Lists]: python-markdown.md#attribute-lists
  [BetterEm]: python-markdown-extensions.md#betterem
  [Caret, Mark & Tilde]: python-markdown-extensions.md#caret-mark-tilde
  [Critic]: python-markdown-extensions.md#critic
  [Definition Lists]: python-markdown.md#definition-lists
  [Details]: python-markdown-extensions.md#details
  [Emoji]: python-markdown-extensions.md#emoji
  [Footnotes]: python-markdown.md#footnotes
  [Highlight]: python-markdown-extensions.md#highlight
  [Keys]: python-markdown-extensions.md#keys
  [Markdown in HTML]: python-markdown.md#markdown-in-html
  [SmartSymbols]: python-markdown-extensions.md#smartsymbols
  [Snippets]: python-markdown-extensions.md#snippets
  [SuperFences]: python-markdown-extensions.md#superfences
  [Tabbed]: python-markdown-extensions.md#tabbed
  [Table of Contents]: python-markdown.md#table-of-contents
  [Tables]: python-markdown.md#tables
  [Tasklist]: python-markdown-extensions.md#tasklist

## 配置 {#configuration}

扩展作为 `mkdocs.yml` -- MkDocs 配置文件的一部分进行配置。以下部分包含两个示例配置，以启动您的文档项目。

  [overview]: #advanced-configuration

### 最小配置 {#minimal-configuration}

这个配置是您第一次使用 Material for MkDocs 时的良好起点。最好的想法是探索[参考文档]，并逐渐添加您想要使用的内容：

``` yaml
markdown_extensions:

  # Python Markdown
  - toc:
      permalink: true

  # Python Markdown Extensions
  - pymdownx.highlight
  - pymdownx.superfences
```

  [参考文档]: ../../reference/index.md

### 推荐配置 {#recommended-configuration}

此配置启用了 Material for MkDocs 的所有与 Markdown 相关的功能，非常适合有经验的用户启动一个新的文档项目：

``` yaml
markdown_extensions:

  # Python Markdown
  - abbr
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - toc:
      permalink: true

  # Python Markdown Extensions
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.details
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
  - pymdownx.highlight
  - pymdownx.inlinehilite
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
  - pymdownx.tasklist:
      custom_checkbox: true
  - pymdownx.tilde
```
