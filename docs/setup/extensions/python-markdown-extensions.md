# Python Markdown 扩展包 {#python-markdown-extensions}

[Python Markdown 扩展包] 是一系列额外扩展的优秀集合，非常适合高级技术写作。MkDocs 材料列表将此包列为显式依赖项，因此在支持版本中自动安装。

  [Python Markdown 扩展包]: https://facelessuser.github.io/pymdown-extensions/

## 支持的扩展 {#supported-extensions}

通常，[Python Markdown 扩展包] 的所有扩展应该都能与 MkDocs 材料一起使用。以下列表包括所有原生支持的扩展，这意味着它们无需进一步调整即可使用。

### Arithmatex

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.arithmatex][Arithmatex] -->

[Arithmatex] 扩展允许渲染块和行内块方程，并与 [MathJax][^1] ——一个数学排版库无缝集成。通过 `mkdocs.yml` 启用：

  [^1]:
    其他库如 [KaTeX] 也受支持，可以通过一些额外努力集成。有关进一步的指导，请参阅 [Arithmatex 关于 KaTeX 的文档]，因为这超出了 MkDocs 材料的范围。

``` yaml
markdown_extensions:
  - pymdownx.arithmatex:
      generic: true
```

除了在 `mkdocs.yml` 中启用扩展外，还需要包括 MathJax 配置和 JavaScript 运行时，这可以通过几行[额外的 JavaScript]来完成：

=== ":octicons-file-code-16: `docs/javascripts/mathjax.js`"

    ``` js
    window.MathJax = {
      tex: {
        inlineMath: [["\\(", "\\)"]],
        displayMath: [["\\[", "\\]"]],
        processEscapes: true,
        processEnvironments: true
      },
      options: {
        ignoreHtmlClass: ".*|",
        processHtmlClass: "arithmatex"
      }
    };

    document$.subscribe(() => { // (1)!
      MathJax.startup.output.clearCache()
      MathJax.typesetClear()
      MathJax.texReset()
      MathJax.typesetPromise()
    })
    ```

    1. 这将 MathJax 与[即时加载]集成


=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/mathjax.js
      - https://polyfill.io/v3/polyfill.min.js?features=es6
      - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
    ```

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [使用块语法]
- [使用行内块语法]

  [Arithmatex]: https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/
  [Arithmatex 关于 KaTeX 的文档]: https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/#loading-katex
  [MathJax]: https://www.mathjax.org/
  [KaTeX]: https://github.com/Khan/KaTeX
  [额外的 JavaScript]: ../../customization.md#additional-javascript
  [即时加载]: ../setting-up-navigation.md#instant-loading
  [使用块语法]: ../../reference/math.md#using-block-syntax
  [使用行内块语法]: ../../reference/math.md#using-inline-block-syntax

### BetterEm

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.betterem][BetterEm] -->

[BetterEm] 扩展改进了使用特殊字符强调 Markdown 中文本的检测，即对 `**bold**` 和 `_italic_` 格式化。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.betterem
```

此扩展的配置选项与 MkDocs 材料无关，因为它们只影响 Markdown 解析阶段。有关更多信息，请参阅 [BetterEm 文档][BetterEm]。

  [BetterEm]: https://facelessuser.github.io/pymdown-extensions/extensions/betterem/

### Caret, Mark & Tilde

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.caret][Caret] -->

[Caret]、[Mark] 和 [Tilde] 扩展增加了使用简单语法突出显示文本并定义下标和上标的功能。通过 `mkdocs.yml` 一起启用它们：

``` yaml
markdown_extensions:
  - pymdownx.caret
  - pymdownx.mark
  - pymdownx.tilde
```

这些扩展的配置选项与 MkDocs 材料无关，因为它们只影响 Markdown 解析阶段。有关指导，请参阅 [Caret]、[Mark] 和 [Tilde 文档][Tilde]。

参考用法：

- [突出显示文本]
- [下标和上标]

  [Caret]: https://facelessuser.github.io/pymdown-extensions/extensions/caret/
  [Mark]: https://facelessuser.github.io/pymdown-extensions/extensions/mark/
  [Tilde]: https://facelessuser.github.io/pymdown-extensions/extensions/tilde/
  [突出显示文本]: ../../reference/formatting.md#highlighting-text
  [下标和上标]: ../../reference/formatting.md#sub-and-superscripts

### Critic

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.critic][Critic] -->

[Critic] 扩展允许使用 [Critic 标记]突出显示文档中添加、删除或更新的部分，即用于跟踪 Markdown 语法中的更改。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.critic
```

支持以下配置选项：

<!-- md:option pymdownx.critic.mode -->

:   <!-- md:default `view` --> 此选项定义如何解析标记，即是仅仅`查看`所有建议的更改，还是`接受`或`拒绝`它们：

    === "查看更改"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: view
        ```

    === "接受更改"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: accept
        ```

    === "拒绝更改"

        ``` yaml
        markdown_extensions:
          - pymdownx.critic:
              mode: reject
        ```

参考用法：

- [突出显示更改]

  [Critic]: https://facelessuser.github.io/pymdown-extensions/extensions/critic/
  [Critic Markup]: https://github.com/CriticMarkup/CriticMarkup-toolkit
  [突出显示更改]: ../../reference/formatting.md#highlighting-changes

### Details

<!-- md:version 1.9.0 -->
<!-- md:extension [pymdownx.details][Details] -->

[Details] 扩展增强了 [Admonition] 扩展，使得生成的 _call-outs_ 可折叠，允许用户打开和关闭。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.details
```

没有可用的配置选项。参考用法：

- [折叠块]

  [Details]: https://facelessuser.github.io/pymdown-extensions/extensions/details/
  [Admonition]: python-markdown.md#admonition
  [折叠块]: ../../reference/admonitions.md#collapsible-blocks

### Emoji

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.emoji][Emoji] -->

[Emoji] 扩展自动将打包的和自定义图标及表情符号以 `*.svg` 文件格式嵌入到生成的 HTML 页面中。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji # (1)!
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

1.  [Python Markdown 扩展包] 使用 `pymdownx` 命名空间，但为了支持图标的嵌入，必须使用 `materialx` 命名空间，因为它扩展了 `pymdownx` 的功能。

支持以下配置选项：

<!-- md:option pymdownx.emoji.emoji_index -->

:   <!-- md:default `emojione` --> 此选项定义用于渲染的表情符号集。请注意，不建议使用 `emojione`，因为[许可限制][Emoji index]：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_index: !!python/name:material.extensions.emoji.twemoji
    ```

<!-- md:option pymdownx.emoji.emoji_generator -->

:   <!-- md:default `to_png` --> 此选项定义如何渲染解析后的表情符号或图标简码。请注意，图标只能与 `to_svg` 配置一起使用：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_generator: !!python/name:material.extensions.emoji.to_svg
    ```

<!-- md:option pymdownx.emoji.options.custom_icons -->

:   <!-- md:default none --> 此选项允许列出文件夹，其中包含可用于 Markdown 或 `mkdocs.yml` 的额外图标集，这在[图标自定义指南]中有更详细的解释：

    ``` yaml
    markdown_extensions:
      - pymdownx.emoji:
          emoji_index: !!python/name:material.extensions.emoji.twemoji
          emoji_generator: !!python/name:material.extensions.emoji.to_svg
          options:
            custom_icons:
              - overrides/.icons
    ```

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [使用表情符号]
- [使用图标]
- [在模板中使用图标]

  [Emoji]: https://facelessuser.github.io/pymdown-extensions/extensions/emoji/
  [Emoji index]: https://facelessuser.github.io/pymdown-extensions/extensions/emoji/#default-emoji-indexes
  [图标自定义指南]: ../changing-the-logo-and-icons.md#additional-icons
  [使用表情符号]: ../../reference/icons-emojis.md#using-emojis
  [使用图标]: ../../reference/icons-emojis.md#using-icons
  [在模板中使用图标]: ../../reference/icons-emojis.md#using-icons-in-templates

### Highlight

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.highlight][Highlight] -->

[Highlight] 扩展增加了对代码块的语法高亮支持（借助 [SuperFences][pymdownx.superfences]）以及对行内代码块的支持（借助 [InlineHilite][pymdownx.inlinehilite]）。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.superfences # (1)!
```

1.  [Highlight] 由 [SuperFences][pymdownx.superfences] 扩展使用，以在代码块上执行语法高亮，而不是相反，这就是为什么还需要启用此扩展的原因。

支持以下配置选项：

<!-- md:option pymdownx.highlight.use_pygments -->

:   <!-- md:default `true` --> 此选项允许控制是否在构建时使用 [Pygments] 进行高亮，或者在浏览器中使用 JavaScript 语法高亮器：

    === "Pygments"

        ``` yaml
        markdown_extensions:
          - pymdownx.highlight:
              use_pygments: true
          - pymdownx.superfences
        ```

    === "JavaScript"

        ``` yaml
        markdown_extensions:
          - pymdownx.highlight:
              use_pygments: false
        ```

        例如，[Highlight.js]，一个 JavaScript 语法高亮器，可以通过一些[额外的 JavaScript]和一个[额外的样式表]在 `mkdocs.yml` 中集成：

        === ":octicons-file-code-16: `docs/javascripts/highlight.js`"

            ``` js
            document$.subscribe(() => {
              hljs.highlightAll()
            })
            ```

        === ":octicons-file-code-16: `mkdocs.yml`"

            ``` yaml
            extra_javascript:
              - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/10.7.2/highlight.min.js
              - javascripts/highlight.js
            extra_css:
              - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/10.7.2/styles/default.min.css
            ```

        请注意，[Highlight.js] 与 [Highlight][pymdownx.highlight] 扩展无关。

    所有后续的配置选项仅与使用 [Pygments] 进行构建时的语法高亮兼容，因此如果设置了 `use_pygments` 为 `false`，则不适用。

<!-- md:option pymdownx.highlight.pygments_lang_class -->

:   <!-- md:default `false` --> 此选项指示 [Pygments] 添加 CSS 类以标识代码块的语言，这对于自定义注释标记的功能至关重要：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      pygments_lang_class: true
```

<!-- md:option pymdownx.highlight.auto_title -->

:   <!-- md:default `false` --> 此选项将自动为所有代码块添加 [title]，显示正在使用的语言的名称，例如，对于 `py` 块显示 `Python`：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          auto_title: true
    ```

<!-- md:option pymdownx.highlight.linenums -->

:   <!-- md:default `false` --> 此选项将为 _所有_ 代码块添加行号。如果您希望为 _某些_ 但不是所有代码块添加行号，请查阅[添加行号][Adding line numbers]的代码块参考部分，其中还包含一些处理行号的技巧：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          linenums: true
    ```

<!-- md:option pymdownx.highlight.linenums_style -->

:   <!-- md:default `table` --> [Highlight] 扩展提供了三种添加行号的方式，其中两种由 MkDocs 材料支持。虽然 `table` 将代码块包裹在一个 `<table>` 元素中，`pymdownx-inline` 将行号作为行本身的一部分渲染：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          linenums_style: pymdownx-inline
    ```

    请注意，`inline` 会将行号放在实际代码旁边，这意味着在用光标选择文本或复制代码块到剪贴板时，行号会被包括在内。因此，建议使用 `table` 或 `pymdownx-inline`。

<!-- md:option pymdownx.highlight.anchor_linenums -->

:   <!-- md:version 8.1.0 --> :octicons-milestone-24:
    默认值：`false` – 如果代码块包含行号，启用此设置将用锚链接包裹它们，以便可以轻松地进行超链接和分享：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          anchor_linenums: true
    ```

<!-- md:option pymdownx.highlight.line_spans -->

:   <!-- md:default none --> 当设置此选项时，代码块的每一行都会被包裹在一个 `span` 中，这对于诸如行高亮等功能至关重要：

    ``` yaml
    markdown_extensions:
      - pymdownx.highlight:
          line_spans: __span
    ```

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [使用代码块]
- [添加标题]
- [添加行号]
- [高亮特定行]
- [自定义语法主题]

  [Highlight]: https://facelessuser.github.io/pymdown-extensions/extensions/highlight/
  [CodeHilite]: python-markdown.md#codehilite
  [pymdownx.superfences]: #superfences
  [pymdownx.inlinehilite]: #inlinehilite
  [Pygments]: https://pygments.org
  [additional style sheet]: ../../customization.md#additional-css
  [Highlight.js]: https://highlightjs.org/
  [title]: ../../reference/code-blocks.md#adding-a-title
  [添加行号]: ../../reference/code-blocks.md#adding-line-numbers
  [使用代码块]: ../../reference/code-blocks.md#usage
  [添加标题]: ../../reference/code-blocks.md#adding-a-title
  [高亮特定行]: ../../reference/code-blocks.md#highlighting-specific-lines
  [自定义语法主题]: ../../reference/code-blocks.md#custom-syntax-theme

### InlineHilite

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.inlinehilite][InlineHilite] -->

[InlineHilite] 扩展增加了对行内代码块的语法高亮支持。它建立在 [Highlight][pymdownx.highlight] 扩展之上，从中获取其配置。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.highlight
  - pymdownx.inlinehilite
```

此扩展的配置选项并非专门针对 MkDocs 材料，因为它们只影响 Markdown 解析阶段。唯一的例外是 [`css_class`][InlineHilite options] 选项，此选项不得更改。有关指导，请参阅 [InlineHilite 文档][InlineHilite]。

参考用法：

- [高亮行内代码块]

  [InlineHilite]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/
  [InlineHilite options]: https://facelessuser.github.io/pymdown-extensions/extensions/inlinehilite/#options
  [pymdownx.highlight]: #highlight
  [高亮行内代码块]: ../../reference/code-blocks.md#highlighting-inline-code-blocks

### Keys

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.keys][Keys] -->

[Keys] 扩展添加了一个简单的语法，用于渲染键盘按键和组合，例如 ++ctrl+alt+del++。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.keys
```

此扩展的配置选项并非专门针对 MkDocs 材料，因为它们只影响 Markdown 解析阶段。唯一的例外是 [`class`][Keys options] 选项，此选项不得更改。有关更多信息，请参阅 [Keys 文档][Keys]。

参考用法：

- [添加键盘按键]

  [Keys]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/
  [Keys options]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/#options
  [添加键盘按键]: ../../reference/formatting.md#adding-keyboard-keys

### SmartSymbols

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.smartsymbols][SmartSymbols] -->

[SmartSymbols] 扩展将某些字符序列转换为相应的符号，例如版权符号或分数。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.smartsymbols
```

此扩展的配置选项并非专门针对 MkDocs 材料，因为它们只影响 Markdown 解析阶段。有关指导，请参阅 [SmartSymbols 文档][SmartSymbols]。

  [SmartSymbols]: https://facelessuser.github.io/pymdown-extensions/extensions/smartsymbols/

### Snippets

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.snippets][Snippets] -->

[Snippets] 扩展添加了一种能力，可以使用简单的语法将内容从任意文件嵌入到文档中，包括其他文档或源文件。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.snippets
```

此扩展的配置选项并非专门针对 MkDocs 材料，因为它们只影响 Markdown 解析阶段。有关更多信息，请参阅 [Snippets 文档][Snippets]。

参考用法：

- [添加词汇表]
- [嵌入外部文件]

  [Snippets]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/
  [添加词汇表]: ../../reference/tooltips.md#adding-a-glossary
  [嵌入外部文件]: ../../reference/code-blocks.md#embedding-external-files

### SuperFences

<!-- md:version 0.1.0 -->
<!-- md:extension [pymdownx.superfences][SuperFences] -->

[SuperFences] 扩展允许在彼此之间任意嵌套代码块和内容块，包括警告、标签页、列表和所有其他元素。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.superfences
```

支持以下配置选项：

<!-- md:option pymdownx.superfences.custom_fences -->

:   <!-- md:default none --> 此选项允许定义自定义栅栏的处理程序，例如为了保留 [Mermaid.js] 图表的定义以在浏览器中解释：

    ``` yaml
    markdown_extensions:
      - pymdownx.superfences:
          custom_fences:
            - name: mermaid
              class: mermaid
              format: !!python/name:pymdownx.superfences.fence_code_format
    ```

    请注意，这主要是为了防止应用语法高亮。参阅 [图表] 参考了解如何将 Mermaid.js 与 MkDocs 材料集成。

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [使用注释]
- [使用代码块]
- [使用内容标签页]
- [使用流程图]
- [使用序列图]
- [使用状态图]
- [使用类图]
- [使用实体关系图]

  [SuperFences]: https://facelessuser.github.io/pymdown-extensions/extensions/superfences/
  [Fenced Code Blocks]: python-markdown.md#fenced-code-blocks
  [Mermaid.js]: https://mermaid-js.github.io/mermaid/
  [diagrams]: ../../reference/diagrams.md
  [使用注释]: ../../reference/annotations.md#usage
  [使用内容标签页]: ../../reference/content-tabs.md#usage
  [使用流程图]: ../../reference/diagrams.md#using-flowcharts
  [使用序列图]: ../../reference/diagrams.md#using-sequence-diagrams
  [使用状态图]: ../../reference/diagrams.md#using-state-diagrams
  [使用类图]: ../../reference/diagrams.md#using-class-diagrams
  [使用实体关系图]: ../../reference/diagrams.md#using-entity-relationship-diagrams

### Tabbed

<!-- md:version 5.0.0 -->
<!-- md:extension [pymdownx.tabbed][Tabbed] -->

[Tabbed] 扩展允许使用内容标签页，这是一种简单的方法，可以将相关内容和代码块组织在可访问的标签下。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.tabbed:
      alternate_style: true
```

支持以下配置选项：

<!-- md:option pymdownx.tabbed.alternate_style -->

:   <!-- md:version 7.3.1 --> <!-- md:default `false` -->
    <!-- md:flag required -->  此选项启用内容标签页的[替代样式]，该样式在[移动视口上更好的行为]，并且是唯一支持的样式：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          alternate_style: true
    ```

<!-- md:option pymdownx.tabbed.combine_header_slug -->

:   <!-- md:default `false` --> 此选项启用内容标签的[combine_header_slug 样式]标志，该标志将标题的 id 添加到标签的 id 前：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          combine_header_slug: true
    ```

<!-- md:option pymdownx.tabbed.slugify -->

:   <!-- md:default `None` --> 此选项允许自定义 slug 函数。对于某些语言，默认可能不会生成良好和可读的标识符 - 考虑使用另一个 slug 函数，例如那些来自 [Python Markdown Extensions][Slugs] 的：

    === "Unicode"

        ``` yaml
        markdown_extensions:
          - pymdownx.tabbed:
              slugify: !!python/object/apply:pymdownx.slugs.slugify
                kwds:
                  case: lower
        ```

    === "Unicode, case-sensitive"

        ``` yaml
        markdown_extensions:
          - pymdownx.tabbed:
              slugify: !!python/object/apply:pymdownx.slugs.slugify {}
        ```

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [组织代码块]
- [组织其他内容]
- [嵌入内容]

  [Tabbed]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/
  [替代样式]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/#alternate-style
  [combine_header_slug 样式]: https://facelessuser.github.io/pymdown-extensions/extensions/tabbed/#tab-ids
  [移动视口上更好的行为]: https://twitter.com/squidfunk/status/1424740370596958214
  [组织代码块]: ../../reference/content-tabs.md#grouping-code-blocks
  [组织其他内容]: ../../reference/content-tabs.md#grouping-other-content
  [嵌入内容]: ../../reference/content-tabs.md#embedded-content
  [Slugs]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

### Tasklist

<!-- md:version 1.0.0 -->
<!-- md:extension [pymdownx.tasklist][Tasklist] -->

[Tasklist] 扩展允许使用受 [GitHub 风格的 Markdown] 启发的[任务列表][Tasklist specification]，遵循相同的语法约定。通过 `mkdocs.yml` 启用：

``` yaml
markdown_extensions:
  - pymdownx.tasklist:
      custom_checkbox: true
```

支持以下配置选项：

<!-- md:option pymdownx.tasklist.custom_checkbox -->

:   <!-- md:default `false` --> 此选项切换复选框的渲染样式，用美观的图标替换原生复选框样式，因此推荐使用：

    ``` yaml
    markdown_extensions:
      - pymdownx.tasklist:
          custom_checkbox: true
    ```

<!-- md:option pymdownx.tasklist.clickable_checkbox -->

:   <!-- md:default `false` --> 此选项切换复选框是否可点击。由于状态不会保持，从用户体验角度来看，使用此选项被 _不鼓励_：

    ``` yaml
    markdown_extensions:
      - pymdownx.tasklist:
          clickable_checkbox: true
    ```

这个扩展的其他配置选项不是 MkDocs 材料官方支持的，因此可能会产生意外的结果。风险自负。

参考用法：

- [使用任务列表]

  [Tasklist]: https://facelessuser.github.io/pymdown-extensions/extensions/tasklist/
  [GitHub 风格的 Markdown]: https://github.github.com/gfm/
  [Tasklist specification]: https://github.github.com/gfm/#task-list-items-extension-
  [使用任务列表]: ../../reference/lists.md#using-task-lists
