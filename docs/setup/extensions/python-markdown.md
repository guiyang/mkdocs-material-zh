# Python Markdown

Material for MkDocs 支持大量 [Python Markdown] 扩展，这是它非常适合技术写作的部分原因。以下是所有支持的扩展的列表，链接到参考资料中的相关部分以了解需要启用哪些功能。

  [Python Markdown]: https://python-markdown.github.io/

## 支持的扩展 {#supported-extensions}

### 缩写 {#abbreviations}

<!-- md:version 1.0.0 -->
<!-- md:extension [abbr][缩写] -->

[缩写] 扩展通过用 `abbr` 标签包装元素，添加能够添加一个小工具提示的功能。只支持纯文本（无标记）。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - abbr
```

没有可用的配置选项。参考使用：

- [添加缩写]
- [添加术语表]

  [缩写]: https://python-markdown.github.io/extensions/abbreviations/
  [添加缩写]: ../../reference/tooltips.md#adding-abbreviations
  [添加术语表]: ../../reference/tooltips.md#adding-a-glossary

### 警告 {#admonition}

<!-- md:version 0.1.0 -->
<!-- md:extension [admonition][警告] -->

[警告] 扩展添加对警告的支持，更常见的称为 _call-outs_，可以通过使用简单的语法在 Markdown 中定义。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - admonition
```

没有可用的配置选项。参考使用：

- [添加警告]
- [更改标题]
- [移除标题]
- [支持的类型]

  [警告]: https://python-markdown.github.io/extensions/admonition/
  [添加警告]: ../../reference/admonitions.md#usage
  [更改标题]: ../../reference/admonitions.md#changing-the-title
  [移除标题]: ../../reference/admonitions.md#removing-the-title
  [支持的类型]: ../../reference/admonitions.md#supported-types

### 属性列表 {#attribute-lists}

<!-- md:version 0.1.0 -->
<!-- md:extension [attr_list][属性列表] -->

[属性列表] 扩展允许为 [几乎每一个][属性列表限制] Markdown 内联和块级元素添加 HTML 属性和 CSS 类，使用特殊语法。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - attr_list
```

没有可用的配置选项。参考使用：

- [使用注释][Using annotations]
- [使用网格]
- [添加按钮]
- [添加工具提示]
- [使用彩色图标]
- [使用动画图标]
- [Image alignment]
- [Image lazy-loading]

  [属性列表]: https://python-markdown.github.io/extensions/attr_list/
  [属性列表限制]: https://python-markdown.github.io/extensions/attr_list/#limitations
  [使用网格]: ../../reference/grids.md#using-grids
  [添加按钮]: ../../reference/buttons.md#adding-buttons
  [添加工具提示]: ../../reference/tooltips.md#adding-tooltips
  [使用彩色图标]: ../../reference/icons-emojis.md#with-colors
  [使用动画图标]: ../../reference/icons-emojis.md#with-animations
  [图像对齐]: ../../reference/images.md#image-alignment
  [图像懒加载]: ../../reference/images.md#image-lazy-loading

### 定义列表 {#definition-lists}

<!-- md:version 1.1.0 -->
<!-- md:extension [def_list][定义列表] -->

[定义列表] 扩展添加了通过 Markdown 向文档添加定义列表（更常见的称为 [描述列表] – `dl` 在 HTML 中）的能力。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - def_list
```

没有可用的配置选项。参考使用：

- [使用定义列表]

  [定义列表]: https://python-markdown.github.io/extensions/definition_lists/
  [描述列表]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dl
  [使用定义列表]: ../../reference/lists.md#using-definition-lists

### 脚注 {#footnotes}

<!-- md:version 1.0.0 -->
<!-- md:extension [footnotes][脚注] -->

[脚注] 扩展允许定义内联脚注，然后在文档的所有 Markdown 内容下方渲染。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - footnotes
```

不支持配置选项。参考使用：

- [添加脚注引用]
- [添加脚注内容]

  [脚注]: https://python-markdown.github.io/extensions/footnotes/
  [添加脚注引用]: ../../reference/footnotes.md#adding-footnote-references
  [添加脚注内容]: ../../reference/footnotes.md#adding-footnote-content

### HTML 中的 Markdown {#markdown-in-html}

<!-- md:version 0.1.0 -->
<!-- md:extension [md_in_html][HTML 中的 Markdown] -->

[HTML 中的 Markdown] 扩展允许在 HTML 中编写 Markdown，这对于使用自定义元素包装 Markdown 内容很有用。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - md_in_html
```

> 默认情况下，Markdown 忽略在原始 HTML 块级元素内的任何内容。通过启用 `md_in_html` 扩展，可以通过在打开标签上包含一个 `markdown` 属性来解析原始 HTML 块级元素的内容为 Markdown。输出时将会删除 `markdown` 属性，而所有其他属性将被保留。

没有可用的配置选项。参考使用：

- [使用注释]
- [使用网格]
- [图像标题]

  [HTML 中的 Markdown]: https://python-markdown.github.io/extensions/md_in_html/
  [使用注释]: ../../reference/annotations.md#usage
  [使用网格]: ../../reference/grids.md#usage
  [图像标题]: ../../reference/images.md#image-captions

### 目录 {#table-of-contents}

<!-- md:version 0.1.0 -->
<!-- md:extension [toc][目录] -->

[目录] 扩展自动从文档生成目录，Material for MkDocs 将其渲染为结果页面的一部分。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - toc:
      permalink: true
```

支持以下配置选项：

<!-- md:option toc.title -->

:   <!-- md:version 7.3.5 --> <!-- md:default computed --> –
    此选项设置右侧导航栏中目录的标题，通常会自动从 `mkdocs.yml` 中设置的 [网站语言] 的翻译中获取：

    ``` yaml
    markdown_extensions:
      - toc:
          title: On this page
    ```

<!-- md:option toc.permalink -->

:   <!-- md:default `false` --> 此选项在每个标题的末尾添加一个包含段落符号 `¶` 或其他自定义符号的锚链接，正如您当前正在查看的页面那样，Material for MkDocs 将在悬停时使其出现：

    === "¶"

        ``` yaml
        markdown_extensions:
          - toc:
              permalink: true
        ```

    === "⚓︎"

        ``` yaml
        markdown_extensions:
          - toc:
              permalink: ⚓︎
        ```

<!-- md:option toc.permalink_title -->

:   <!-- md:default `Permanent link` --> 此选项设置悬停时显示的锚链接的标题，并由屏幕阅读器阅读。出于可访问性的原因，更改为更可辨别的名称可能会有益，说明锚链接指向该部分本身：

    ``` yaml
    markdown_extensions:
      - toc:
          permalink_title: Anchor link to this section for reference
    ```

<!-- md:option toc.slugify -->

:   <!-- md:default `toc.slugify` --> 此选项允许自定义 slug 函数。对于某些语言，缺省值可能无法产生良好的可读标识符 - 考虑使用其他 slug 函数，例如 [Python Markdown Extensions][Slugs] 中的函数：

    === "Unicode"

        ``` yaml
        markdown_extensions:
          - toc:
              slugify: !!python/object/apply:pymdownx.slugs.slugify
                kwds:
                  case: lower
        ```

    === "Unicode, case-sensitive"

        ``` yaml
        markdown_extensions:
          - toc:
              slugify: !!python/object/apply:pymdownx.slugs.slugify {}
        ```

<!-- md:option toc.toc_depth -->

:   <!-- md:default `6` --> 定义要包含在目录中的级别范围。这对于具有深层结构的标题的项目文档可能很有用，以减少目录的长度，或完全删除目录：

    === "隐藏级别 4-6"

        ``` yaml
        markdown_extensions:
          - toc:
              toc_depth: 3
        ```

    === "隐藏目录"

        ``` yaml
        markdown_extensions:
          - toc:
              toc_depth: 0
        ```

此扩展的其他配置选项未被 Material for MkDocs 官方支持，因此可能产生意外结果。风险自负。

  [目录]: https://python-markdown.github.io/extensions/toc/
  [网站语言]: ../changing-the-language.md#site-language
  [Slugs]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

### 表格 {#tables}

<!-- md:version 0.1.0 -->
<!-- md:extension [tables][表格] -->

[表格] 扩展通过使用简单的语法在 Markdown 中添加创建表格的功能。通过 `mkdocs.yml` 启用（尽管它应该默认启用）：

``` yaml
markdown_extensions:
  - tables
```

没有可用的配置选项。参考使用：

- [使用数据表]
- [列对齐]

  [表格]: https://python-markdown.github.io/extensions/tables/
  [使用数据表]: ../../reference/data-tables.md#usage
  [列对齐]: ../../reference/data-tables.md#column-alignment

## 不再支持的扩展 {#superseded-extensions}

以下 [Python Markdown] 扩展不再（或可能不再）受支持，因此不建议使用。相反，应考虑替代品。

### 围栏代码块 {#fenced-code-blocks}

<!-- md:version 0.1.0 -->
<!-- md:extension [fenced_code_blocks][围栏代码块] -->

被 [SuperFences] 取代。这个扩展可能仍然可以工作，但是 [SuperFences] 扩展在许多方面都优越，因为它允许任意嵌套，因此推荐使用。

  [围栏代码块]: https://python-markdown.github.io/extensions/fenced_code_blocks/
  [SuperFences]: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/

### CodeHilite

<!-- md:version 0.1.0 -->
<!-- md:extension [codehilite][CodeHilite] -->

被 [Highlight] 取代。支持 CodeHilite 已在
<!-- md:version 6.0.0 --> 中删除，因为 [Highlight] 与其他基本扩展如 [SuperFences] 和 [InlineHilite] 有更好的集成。

  [CodeHilite]: https://python-markdown.github.io/extensions/code_hilite/
  [CodeHilite support]: https://github.com/squidfunk/mkdocs-material/releases/tag/0.1.0
  [Highlight]: https://facelessuser.github.io/pymdown-extensions/extensions/highlight/
  [InlineHilite]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/
