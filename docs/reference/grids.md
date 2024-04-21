---
icon: material/view-grid-plus
---

# 网格 Grids {#grids}

Material for MkDocs 使得将部分内容安排成网格变得简单，将传达类似意义或同等重要性的块组合在一起。网格非常适合构建展示大部分文档概述的索引页面。

## 配置 {#configuration}

此配置启用网格的使用，允许将相同或不同类型的块组合成矩形形状。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions: # (1)!
  - attr_list
  - md_in_html
```

1.  请注意，下面列出的一些示例使用了[图标和表情]，这些需要[单独配置]。

查看其他配置选项：

- [属性列表]
- [HTML 中的 Markdown]

  [图标和表情]: icons-emojis.md
  [单独配置]: icons-emojis.md#configuration
  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [HTML 中的 Markdown]: ../setup/extensions/python-markdown.md#markdown-in-html

## 用法 {#usage}

网格有两种风格：[卡片网格]和[通用网格]。卡片网格将每个元素包裹在一个悬浮卡片中，而通用网格允许以矩形形状排列任意块元素。

  [卡片网格]: #using-card-grids
  [通用网格]: #using-generic-grids

### 使用卡片网格 {#using-card-grids}

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

卡片网格将每个网格项包裹在一个美观的悬浮卡片中，当鼠标悬停时卡片会浮起。它们有两种略有不同的语法：[列表]和[块语法]，支持不同的使用场景。

  [列表]: #list-syntax
  [块语法]: #block-syntax

#### 列表语法 {#list-syntax}

列表语法本质上是 [卡片网格] 的快捷方式，包括一个由带有 `grid` 和 `cards` 类的 `div` 包裹的无序（或有序）列表：

``` html title="Card grid"
<div class="grid cards" markdown>

- :fontawesome-brands-html5: __HTML__ 用于内容和结构
- :fontawesome-brands-js: __JavaScript__ 用于互动性
- :fontawesome-brands-css3: __CSS__ 文本溢出盒子
- :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 呃？

</div>
```

<div class="result" markdown>
  <div class="grid cards" markdown>

- :fontawesome-brands-html5: __HTML__ 用于内容和结构
- :fontawesome-brands-js: __JavaScript__ 用于互动性
- :fontawesome-brands-css3: __CSS__ 文本溢出盒子
- :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 呃？

  </div>
</div>

列表元素可以包含任意 Markdown，只要外围的 `div` 定义了 `markdown` 属性。下面是一个更复杂的示例，其中包括图标和链接：

``` html title="Card grid, complex example"
<div class="grid cards" markdown>

-   :material-clock-fast:{ .lg .middle } __五分钟内设置__

    ---

    使用 [`pip`][pip] 安装 [`mkdocs-material`][mkdocs-material] 并在几分钟内启动运行

    [:octicons-arrow-right-24: 开始入门][getting started]

-   :fontawesome-brands-markdown:{ .lg .middle } __就是 Markdown__

    ---

    专注于你的内容并生成一个响应式且可搜索的静态网站

    [:octicons-arrow-right-24: 参考][reference]

-   :material-format-font:{ .lg .middle } __量身定做__

    ---

    只需几行代码即可更改颜色、字体、语言、图标、logo 等

    [:octicons-arrow-right-24: 自定义][customization]

-   :material-scale-balance:{ .lg .middle } __开源，MIT__

    ---

    Material for MkDocs 在 MIT 许可下授权并可在 [GitHub] 上获取

    [:octicons-arrow-right-24: 许可证][license]

</div>
```

<div class="result" markdown>
  <div class="grid cards" markdown>

-   :material-clock-fast:{ .lg .middle } __五分钟内设置__

    ---

    使用 [`pip`][pip] 安装 [`mkdocs-material`][mkdocs-material] 并在几分钟内启动运行

    [:octicons-arrow-right-24: 开始入门][getting started]

-   :fontawesome-brands-markdown:{ .lg .middle } __就是 Markdown__

    ---

    专注于你的内容并生成一个响应式且可搜索的静态网站

    [:octicons-arrow-right-24: 参考][reference]

-   :material-format-font:{ .lg .middle } __量身定做__

    ---

    只需几行代码即可更改颜色、字体、语言、图标、logo 等

    [:octicons-arrow-right-24: 自定义][customization]

-   :material-scale-balance:{ .lg .middle } __开源，MIT__

    ---

    Material for MkDocs 在 MIT 许可下授权并可在 [GitHub] 上获取

    [:octicons-arrow-right-24: 许可证][license]

  </div>
</div>

如果没有足够的空间将网格项并排渲染，这些项将扩展到视口的整个宽度，例如在移动视口上。如果有更多空间可用，网格将渲染 3 个及以上的项目，例如当[隐藏两侧边栏]时。

  [mkdocs-material]: https://pypistats.org/packages/mkdocs-material
  [pip]: ../getting-started.md#with-pip
  [getting started]: ../getting-started.md
  [reference]: ../reference/index.md
  [customization]: ../customization.md
  [license]: ../license.md
  [GitHub]: https://github.com/squidfunk/mkdocs-material
  [隐藏两侧边栏]: ../setup/setting-up-navigation.md#hiding-the-sidebars

#### 块语法 {#block-syntax}

块语法允许将卡片与其他元素一起在网格中排列，如[通用网格]部分所述。只需在 `grid` 中的任何块元素上添加 `card` 类：

``` html title="Card grid, blocks"
<div class="grid" markdown>

:fontawesome-brands-html5: __HTML__ 用于内容和结构
{ .card }

:fontawesome-brands-js: __JavaScript__ 用于互动性
{ .card }

:fontawesome-brands-css3: __CSS__ 文本溢出盒子
{ .card }

> :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 呃？

</div>
```

<div class="result" markdown>
  <div class="grid" markdown>

:fontawesome-brands-html5: __HTML__ 用于内容和结构
{ .card }

:fontawesome-brands-js: __JavaScript__ 用于互动性
{ .card }

:fontawesome-brands-css3: __CSS__ 文本溢出盒子
{ .card }

> :fontawesome-brands-internet-explorer: __Internet Explorer__ ... 呃？

  </div>
</div>

虽然这种语法起初看起来可能过于冗长，但前面的示例显示了如何将卡片网格与其他将也会扩展到网格的元素混合使用。

### 使用通用网格 {#using-generic-grids}

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

通用网格允许在网格中排列任意块元素，包括[警告]、[代码块]、[内容标签页]等。只需使用带有 `grid` 类的 `div` 包裹一组块：

```` html title="Generic grid"
<div class="grid" markdown>

=== "Unordered list"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "Ordered list"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

``` title="Content tabs"
=== "Unordered list"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "Ordered list"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

</div>
````

<div class="result" markdown>
  <div class="grid" markdown>

=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

``` title="Content tabs"
=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

  </div>
</div>

  [警告]: admonitions.md
  [代码块]: code-blocks.md
  [内容标签页]: content-tabs.md
