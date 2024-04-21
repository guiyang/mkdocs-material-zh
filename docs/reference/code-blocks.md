---
icon: material/code-json
---

# 代码块 Code blocks {#code-blocks}

代码块和示例是技术项目文档的重要组成部分。Material for MkDocs 提供了不同的方式来设置代码块的语法高亮，可以在构建时使用 [Pygments] 或在运行时使用 JavaScript 语法高亮器。

  [Pygments]: https://pygments.org

## 配置 {#configuration}

此配置启用代码块和内联代码块的语法高亮，并允许直接从其他文件包含源代码。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences
```

以下部分讨论如何使用 [Pygments]（推荐的高亮器）来使用不同的语法高亮功能，这些功能在使用 JavaScript 语法高亮器时不适用。

查看其他配置选项：

- [Highlight]
- [InlineHilite]
- [SuperFences]
- [Snippets]

  [Highlight]: ../setup/extensions/python-markdown-extensions.md#highlight
  [InlineHilite]: ../setup/extensions/python-markdown-extensions.md#inlinehilite
  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences
  [Snippets]: ../setup/extensions/python-markdown-extensions.md#snippets

### 代码复制按钮 {#code-copy-button}

<!-- md:version 9.0.0 -->
<!-- md:feature -->

代码块可以自动在右侧渲染一个按钮，允许用户将代码块的内容复制到剪贴板。将以下内容添加到 `mkdocs.yml` 以全局启用它们：

``` yaml
theme:
  features:
    - content.code.copy
```

??? info "为特定代码块启用或禁用代码复制按钮"

    如果您不想全局启用代码复制按钮，可以使用基于 [属性列表] 扩展的稍有不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .copy }
    # Code block content
    ```
    ````

    注意语言简码必须首先出现，现在还必须加上 `.` 前缀。同样，复制按钮也可以为特定代码块禁用：

    ```` { .yaml .no-copy }
    ``` { .yaml .no-copy }
    # Code block content
    ```
    ````

### 代码选择按钮 {#code-selection-button}

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

代码块可以包含一个按钮，允许用户选择行范围，这对于链接到代码块的特定子部分非常完美。这允许用户动态应用 [行高亮]。将以下内容添加到 `mkdocs.yml` 以全局启用它：

``` yaml
theme:
  features:
    - content.code.select
```

??? info "为特定代码块启用或禁用代码选择按钮"

    如果您不想全局启用代码选择按钮，可以使用基于 [属性列表] 扩展的稍有不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .select }
    # Code block content
    ```
    ````

    注意语言简码必须首先出现，现在还必须加上 `.` 前缀。同样，选择按钮也可以为特定代码块禁用：

    ```` { .yaml .no-select }
    ``` { .yaml .no-select }
    # Code block content
    ```
    ````

  [行高亮]: #highlighting-specific-lines

### 代码注释 {#code-annotations}

<!-- md:version 8.0.0 -->
<!-- md:feature -->

代码注释通过在代码块的块注释和内联注释中添加数字标记，提供了一种舒适和友好的方式来附加任意内容到代码块的特定部分。将以下内容添加到 `mkdocs.yml` 以全局启用它们：

``` yaml
theme:
  features:
    - content.code.annotate # (1)!
```

1.  :man_raising_hand: 我是代码注释！我可以包含 `代码`、__格式化文本__、图片……基本上任何可以用 Markdown 编写的内容。

??? info "为特定代码块启用代码注释"

    如果您不想全局启用代码注释，因为您不喜欢自动内联行为，您可以使用基于 [属性列表] 扩展的稍有不同的语法为特定代码块启用它们：

    ```` yaml
    ``` { .yaml .annotate }
    # Code block content
    ```
    ````

    注意语言简码必须首先出现，现在还必须加上 `.` 前缀。

  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists

#### 自定义选择器

<!-- md:sponsors -->
<!-- md:version insiders-4.32.0 -->
<!-- md:flag experimental -->

通常，代码注释只能[放置在注释中]，因为注释被认为是安全的放置位置。然而，有时可能需要在不允许注释的代码块部分放置注释，例如在字符串中。

可以为每种语言设置额外的选择器：

``` yaml
extra:
  annotate:
    json: [.s2] # (1)!
```

1.  [`.s2`][s2] 是 [Pygments] 为双引号字符串生成的词法名。如果您想在注释以外的其他词法中使用代码注释，请检查代码块并确定需要添加到额外选择器列表中的词法名。

    __重要__：代码注释不能跨词法分割。

现在，代码注释可以在 JSON 字符串中使用：

``` json
{
  "key": "value (1)"
}
```

1.  :man_raising_hand: 我是代码注释！我可以包含 `代码`、__格式化文本__、图片……基本上任何可以用 Markdown 编写的内容。

  [放置在注释中]: #adding-annotations
  [s2]: https://github.com/squidfunk/mkdocs-material/blob/87d5ca487b9d9ab95c41ee72813149d214048693/src/assets/stylesheets/main/extensions/pymdownx/_highlight.scss#L45

## 用法

代码块必须用包含三个反引号的两行单独封闭。要为这些块添加语法高亮，请在打开块后直接添加语言简码。查看[可用词法器列表]以找到给定语言的简码：

```` markdown title="Code block"
``` py
import tensorflow as tf
```
````

<div class="result" markdown>

``` py
import tensorflow as tf
```

</div>

  [可用词法器列表]: https://pygments.org/docs/lexers/

### 添加标题

为了提供额外的上下文，可以通过在简码后直接使用 `title="<custom title>"` 选项为代码块添加自定义标题，例如显示文件名：

```` markdown title="Code block with title"
``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

<div class="result" markdown>

``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

</div>

### 添加注释

代码注释可以放置在可以放置该块语言注释的代码块的任何位置，例如对于 JavaScript 在 `#!js // ...` 和 `#!js /* ... */`，对于 YAML 在 `#!yaml # ...` 等 [^1]：

  [^1]:
    代码注释需要使用 [Pygments] 进行语法高亮 — 它们当前与 JavaScript 语法高亮器或没有注释语法的语言不兼容。然而，我们正在积极研究支持定义代码注释的替代方式，允许始终在行尾放置代码注释。

```` markdown title="Code block with annotation"
``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.
````

<div class="result" markdown>

``` yaml
theme:
  features:
    - content.code.annotate # (1)
```

1.  :man_raising_hand: 我是代码注释！我可以包含 `代码`、__格式化文本__、图片……基本上任何可以用 Markdown 编写的内容。

</div>

#### 去除注释

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->

如果您希望去除围绕代码注释的注释字符，请在代码注释的闭合括号后添加 `!`：

```` markdown title="Code block with annotation, stripped"
``` yaml
# (1)!
```

1.  Look ma, less line noise!
````

<div class="result" markdown>

``` yaml
# (1)!
```

1.  Look ma, less line noise!

</div>

请注意，这只允许每个注释渲染一个代码注释。如果您想添加多个代码注释，由于技术原因，注释不能被去除。

### 添加行号

可以通过在简码后直接使用 `linenums="<start>"` 选项为代码块添加行号，其中 `<start>` 代表起始行号。代码块可以从 `1` 以外的行号开始，这有助于分割大型代码块以提高可读性：

```` markdown title="Code block with line numbers"
``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
````

<div class="result" markdown>

``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

</div>

### 高亮特定行

通过在语言简码后直接传递行号到 `hl_lines` 参数来高亮特定行。请注意，无论作为 [`linenums`][添加行号] 的一部分指定的起始行号是多少，行计数始终从 `1` 开始：

=== "行"

    ```` markdown title="Code block with highlighted lines"
    ``` py hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````

    <div class="result" markdown>

    ``` py linenums="1" hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

    </div>

=== "行范围"

    ```` markdown title="Code block with highlighted line range"
    ``` py hl_lines="3-5"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```
    ````

    <div class="result" markdown>

    ``` py linenums="1" hl_lines="3-5"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

    </div>

  [添加行号]: #adding-line-numbers

### 高亮内联代码块

当启用 [InlineHilite] 时，可以通过在内联代码块前加上一个 `#!`（直接跟着相应的[语言简码][可用词法器列表]）应用语法高亮。

``` markdown title="Inline code block"
The `#!python range()` function is used to generate a sequence of numbers.
```

<div class="result" markdown>

The `#!python range()` function is used to generate a sequence of numbers.

</div>

### 嵌入外部文件

当启用 [Snippets] 时，可以通过在代码块中直接使用 [`--8<--` 符号][Snippets 符号] 嵌入其他文件（包括源文件）的内容：

```` markdown title="Code block with external content"
``` title=".browserslistrc"
;--8<-- ".browserslistrc"
```
````

<div class="result" markdown>

``` title=".browserslistrc"
last 4 years
```

</div>

  [Snippets 符号]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#snippets-notation

## 自定义

### 自定义语法主题

如果使用 [Pygments]，Material for MkDocs 提供了[代码块样式][colors]，这些样式使用定制且平衡的调色板构建，同样适用于两种[配色方案]：

- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-number-color) " } `--md-code-hl-number-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-special-color) " } `--md-code-hl-special-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-function-color) " } `--md-code-hl-function-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-constant-color) " } `--md-code-hl-constant-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-keyword-color) " } `--md-code-hl-keyword-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-string-color) " } `--md-code-hl-string-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-name-color) " } `--md-code-hl-name-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-operator-color) " } `--md-code-hl-operator-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-punctuation-color) " } `--md-code-hl-punctuation-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-comment-color) " } `--md-code-hl-comment-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-generic-color) " } `--md-code-hl-generic-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-variable-color) " } `--md-code-hl-variable-color`

代码块的前景、背景和行高亮颜色通过以下方式定义：

- :material-checkbox-blank-circle:{ style="color: var(--md-code-fg-color) " } `--md-code-fg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-bg-color) " } `--md-code-bg-color`
- :material-checkbox-blank-circle:{ style="color: var(--md-code-hl-color) " } `--md-code-hl-color`

假设您想改变 `#!js "strings"` 的颜色。虽然有几种[字符串令牌类型]，它们使用相同的颜色。您可以通过使用[额外样式表]分配新颜色：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root > * {
      --md-code-hl-string-color: #0FF1CE;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

如果您想调整特定类型的字符串，例如 ``#!js `backticks` ``，您可以在[语法主题定义]中查找特定的 CSS 类名，并在[额外样式表]中覆盖它：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .highlight .sb {
      color: #0FF1CE;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

  [colors]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/_colors.scss
  [配色方案]: ../setup/changing-the-colors.md#color-scheme
  [字符串令牌类型]: https://pygments.org/docs/tokens/#literals
  [额外样式表]: ../customization.md#additional-css
  [语法主题定义]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/extensions/pymdownx/_highlight.scss

### 注释工具提示宽度

如果您的代码注释中托管了大量内容，通过在[额外样式表]的一部分中增加工具提示的宽度可能是个好主意：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root {
      --md-tooltip-width: 600px;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

这将使注释以更大的宽度呈现：

<div style="--md-tooltip-width: 600px;" markdown>

``` yaml
# (1)!
```

1. Muuuuuuuuuuuuuuuch more space for content
   更多内容空间

</div>
