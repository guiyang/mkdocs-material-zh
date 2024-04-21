---
icon: material/plus-circle
---

# 注释 Annotations {#annotations}

Material for MkDocs 的一大亮点功能是能够注入注释 -- 可以在文档中几乎任何地方添加的小标记，在点击或键盘聚焦时展开包含任意 Markdown 的工具提示。

## 配置 {#configuration}

此配置允许向所有内联和块级元素以及代码块添加注释，并在彼此之间嵌套注释。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
  - pymdownx.superfences
```

查看其他配置选项：

- [属性列表]
- [HTML 中的 Markdown]
- [SuperFences]

  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [HTML 中的 Markdown]: ../setup/extensions/python-markdown.md#markdown-in-html
  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences

### 注释图标 {#annotation-icons}

<!-- md:version 9.2.0 -->

注释图标可以更改为主题捆绑的任何图标，甚至是[自定义图标]，例如 material/arrow-right-circle:. 只需将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  icon:
    annotation: material/arrow-right-circle # (1)!
```

1.  输入几个关键字使用我们的[图标搜索]找到完美的图标，并点击简码复制到您的剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material circle" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

一些流行的选择：

- :material-plus-circle: - `material/plus-circle`
- :material-circle-medium: - `material/circle-medium`
- :material-record-circle: - `material/record-circle`
- :material-arrow-right-circle: - `material/arrow-right-circle`
- :material-arrow-right-circle-outline: - `material/arrow-right-circle-outline`
- :material-chevron-right-circle: - `material/chevron-right-circle`
- :material-star-four-points-circle: - `material/star-four-points-circle`
- :material-plus-circle-outline: - `material/plus-circle-outline`

  [自定义图标]: ../setup/changing-the-logo-and-icons.md#additional-icons
  [图标搜索]: icons-emojis.md#search

## 用法 {#usage}

### 使用注释 {#using-annotations}

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->

注释包括两个部分：可以放置在用 `annotate` 类标记的块中任何位置的标记，以及位于包含标记的块下方列表中的内容：

``` markdown title="Text with annotations"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be expressed in Markdown.
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！我可以包含 `代码`、__格式化文本__、图片......基本上任何可以用 Markdown 编写的内容。

</div>

请注意，`annotate` 类只能添加到最外层的块上。所有嵌套元素都可以使用相同的列表来定义注释，除非注释本身嵌套。

#### 在注释中 {#in-annotations}

当启用 [SuperFences] 时，可以通过将 `annotate` 类添加到托管注释内容的列表项上，重复该过程来嵌套注释：

``` markdown title="Text with nested annotations"
Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: 我是一个注释！(1) { .annotate style="margin-bottom: 0" }

    1.  :woman_raising_hand: 我也是一个注释！

</div>

#### 在警告中 {#in-admonitions}

[警告]的标题和正文也可以通过在类型限定符后添加 `annotate` 修饰符来托管注释，这类似于[行内块]的工作方式：

``` markdown title="Admonition with annotations"
!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: I'm an annotation!
2.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

!!! note annotate "Phasellus posuere in sem ut cursus (1)"

    Lorem ipsum dolor sit amet, (2) consectetur adipiscing elit. Nulla et
    euismod nulla. Curabitur feugiat, tortor non consequat finibus, justo
    purus auctor massa, nec semper lorem quam in massa.

1.  :man_raising_hand: I'm an annotation!
2.  :woman_raising_hand: I'm an annotation as well!

</div>

  [警告]: admonitions.md
  [行内块]: admonitions.md#inline-blocks

#### 在内容标签中 {#in-content-tabs}

内容标签可以通过将 `annotate` 类添加到专用内容标签的块上（而不是不支持的容器上）来托管注释：

``` markdown title="Content tabs with annotations"
=== "Tab 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: I'm an annotation!

=== "Tab 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: I'm an annotation as well!
```

<div class="result" markdown>

=== "Tab 1"

    Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
    { .annotate }

    1.  :man_raising_hand: 我是一个注释！

=== "Tab 2"

    Phasellus posuere in sem ut cursus (1)
    { .annotate }

    1.  :woman_raising_hand: 我也是一个注释！

</div>

#### 在其他所有内容中 {#in-everything-else}

[属性列表] 扩展是将注释添加到大多数元素的关键成分，但它有一些[限制]。然而，始终可以利用 [HTML 中的 Markdown] 扩展将任意元素用 `annotate` 类的 `div` 包装起来：

```` html title="HTML with annotations"
<div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

</div>

1.  :man_raising_hand: I'm an annotation!
````

<div class="result" markdown>
  <div class="annotate" markdown>

> Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.

  </div>

1.  :man_raising_hand: 我是一个注释！

</div>

利用这个技巧，注释也可以添加到引用、列表和许多其他不受 [属性列表] 扩展支持的元素中。此外，请注意[代码块遵循不同的语义]。

!!! warning "已知限制"

    请注意，注释目前不适用于[数据表]，如 #3453 报告的，因为数据表是可滚动元素，定位非常难以正确处理。这可能在将来得到修复。

  [限制]: https://python-markdown.github.io/extensions/attr_list/#limitations
  [代码块遵循不同的语义]: code-blocks.md#adding-annotations
  [数据表]: data-tables.md
