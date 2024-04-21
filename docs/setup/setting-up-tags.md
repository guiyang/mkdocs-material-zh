# 设置标签 {#setting-up-tags}

Material for MkDocs 为页面分类添加了一流的标签支持，这增加了通过搜索和专 dedicated 的[标签索引]对相关页面进行分组的可能性。如果您的文档很大，标签可以帮助更快地发现相关信息。

  [标签索引]: #adding-a-tags-index

## 配置 {#configuration}

### 内置标签插件 {#built-in-tags-plugin}

<!-- md:version 8.2.0 -->
<!-- md:plugin -->

内置标签插件添加了将任何页面与标签分类的能力，作为页面前置元素的一部分。为了添加对标签的支持，请将以下行添加到 `mkdocs.yml` 中：

``` yaml
plugins:
  - tags
```

有关所有设置的列表，请查阅[插件文档]。

  [插件文档]: ../plugins/tags.md

#### 高级设置 {#advanced-settings}

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

以下高级设置目前仅限于我们的[赞助者][Insiders]。它们完全是可选的，并且只会增加标签插件的额外功能：

<!-- - [`listings_layout`][config.listings_layout] -->
- [`listings_toc`][config.listings_toc]

我们将在不久的将来在这里添加更多设置。

  [Insiders]: ../insiders/index.md
  [config.listings_layout]: ../plugins/tags.md#config.listings_layout
  [config.listings_toc]: ../plugins/tags.md#config.listings_toc

### 标签图标和标识符 {#tag-icons-and-identifiers}

<!-- md:version 8.5.0 -->
<!-- md:flag experimental -->
<!-- md:example tags-with-icons -->

每个标签都可以与一个图标关联，然后在标签内部渲染。在为标签分配图标之前，通过在 `mkdocs.yml` 中添加以下内容，将每个标签与一个唯一标识符关联：

``` yaml
extra:
  tags:
    <tag>: <identifier> # (1)!
```

1.  标识符只能包含字母数字字符，以及破折号和下划线。例如，如果您有一个标签 `Compatibility`，您可以设置 `compat` 为标识符：

    ``` yaml
    extra:
      tags:
        Compatibility: compat
    ```

    标识符可以在标签之间重复使用。未显式关联的标签将使用默认标签图标，即 :material-pound:

接下来，可以通过在 `mkdocs.yml` 中的 `theme.icon` 配置设置下添加以下行，将每个标识符与一个图标关联，甚至是[自定义图标]：

=== "标签图标"

    ``` yaml
    theme:
      icon:
        tag:
          <identifier>: <icon> # (1)!
    ```

    1.  使用我们的[图标搜索]输入几个关键字来找到完美的图标，并点击短代码将其复制到剪贴板：

        <div class="mdx-iconsearch" data-mdx-component="iconsearch">
          <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="tag" />
          <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
            <div class="mdx-iconsearch-result__meta"></div>
            <ol class="mdx-iconsearch-result__list"></ol>
          </div>
        </div>

=== "标签默认图标"

    ``` yaml
    theme:
      icon:
        tag:
          default: <icon>
    ```

??? example "展开查看示例"

    ``` yaml
    theme:
      icon:
        tag:
          html: fontawesome/brands/html5
          js: fontawesome/brands/js
          css:  fontawesome/brands/css3
    extra:
      tags:
        HTML5: html
        JavaScript: js
        CSS: css
    ```

  [自定义图标]: changing-the-logo-and-icons.md#additional-icons
  [图标搜索]: ../reference/icons-emojis.md#search

## 使用 {#usage}

### 添加标签 {#adding-tags}

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

启用[内置标签插件]后，可以通过在 Markdown 文件的顶部添加前置元素 `tags` 属性为文档添加标签：

``` sh
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

...
```

页面现在将在主标题上方和搜索预览中呈现这些标签，现在可以 __通过标签找到页面__。

??? question "如何为整个文件夹设置标签？"

    借助[内置元数据插件]，您可以确保通过在相应文件夹中创建 `.meta.yml` 文件并添加以下内容，为整个部分和所有嵌套页面设置标签：

    ``` yaml
    tags:
      - HTML5
      - JavaScript
      - CSS
    ```

    在 `.meta.yml` 中设置的标签将与页面定义的标签合并并去重，这意味着您可以在 `.meta.yml` 中定义通用标签，然后为每个页面添加特定标签。`.meta.yml` 中的标签将被附加。

  [内置标签插件]: ../plugins/tags.md
  [内置元数据插件]: ../plugins/meta.md

### 添加标签索引 {#adding-a-tags-index}

<!-- md:version 8.2.0 -->
<!-- md:example tags -->

[内置标签插件]允许定义一个文件来渲染标签索引，该文件可以是 `nav` 部分的任何页面。要添加标签索引，请创建一个页面，例如 `tags.md`：

``` markdown
# Tags

Following is a list of relevant tags:

<!-- material/tags -->
```

然后在您的 `mkdocs.yml` 文件中添加以下内容。

``` yaml
plugins:
  - tags:
      tags_file: tags.md # (1)!
```

1. 使用 [Insiders] 时不需要此设置。

请注意，`tags.md` 的路径相对于 `docs/` 目录。

标签标记指定了标签索引的位置，即在页面呈现时替换为实际的标签索引。您可以在标记前后包含任意内容：

[![Tags index][tags index enabled]][tags index enabled]

  [tags.tags_file]: #tags-file
  [tags index enabled]: ../assets/screenshots/tags-index.png

### 高级功能 {#advanced-features}

[Insiders] __提供了标签插件的全面重写版本__，比社区版中的当前版本功能更强大。它允许任意数量的标签索引（列表），[范围的列表]、[影子标签]、[嵌套标签]，等等。

  [范围的列表]: #scoped-listings
  [影子标签]: #shadow-tags
  [嵌套标签]: #nested-tags

#### 可配置的列表 {#configurable-listings}

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

列表可以在 `mkdocs.yml` 中或直接在您在 Markdown 文档中放置标记的位置进行配置。一些示例：

- __使用[范围的列表]__：将标签索引限制为与页面位于同一文档子部分级别的页面：

    ``` html
    <!-- material/tags { scope: true } -->
    ```

- __仅列出特定标签__：将标签索引限制为单个或多个选定的标签，例如，`Foo` 和 `Bar`，排除所有其他标签：

    ``` html
    <!-- material/tags { include: [Foo, Bar] } -->
    ```

- __排除带有特定标签的页面__：不包括标有特定标签的页面，例如 `Internal`。这可以是任何标签，包括影子标签：

    ``` html
    <!-- material/tags { exclude: [Internal] } -->
    ```

- __在目录中启用或禁用标签__：指定目录是否列出所有标签在最近的标题下：

    ``` html
    <!-- material/tags { toc: false } -->
    ```

查看[列表配置]了解所有选项。

  [列表配置]: ../plugins/tags.md#listing-configuration

#### 有范围的列表 {#scoped-listings}

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

如果您的文档很大，您可能需要考虑使用有范围的列表，它只包括与包含列表的页面同一级别或以下的页面。只需使用：

``` html
<!-- material/tags { scope: true } -->
```

如果您打算使用多个有范围的索引，最好在 `mkdocs.yml` 中定义一个列表配置，然后通过其 ID 引用它：

``` yaml
plugins:
  - tags:
      listings_map:
        scoped:
          scope: true
```

您现在可以使用：

``` html
<!-- material/tags scoped -->
```

#### 影子标签 {#shadow-tags}

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

影子标签是仅用于组织的标签，可以通过一个简单的标志包括或排除它们的渲染。它们可以在[`shadow_tags`][config.shadow_tags]设置中列举：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

如果一个文档被标记为 `Draft`，则只有在启用[`shadow`][config.shadow]设置时才会渲染该标签，并在禁用时排除。这是使用标签进行结构化的绝佳机会。

  [config.shadow]: ../plugins/tags.md#config.shadow
  [config.shadow_tags]: ../plugins/tags.md#config.shadow_tags

#### 嵌套标签 {#nested-tags}

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:flag experimental -->

[Insiders] 支持嵌套标签。[`tags_hierarchy_separator`][config.tags_hierarchy_separator] 允许创建标签层级，例如 `Foo/Bar`。嵌套标签将作为父标签的子项呈现：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

  [config.tags_hierarchy_separator]: ../plugins/tags.md#config.tags_hierarchy_separator

### 在页面上隐藏标签 {#hiding-tags-on-a-page}

虽然标签在主标题上方呈现，但有时可能希望对特定页面隐藏它们，这可以通过前置元素 `hide` 属性实现：

``` yaml
---
hide:
  - tags
---

# Page title
...
```
