---
title: 内置标签插件
icon: material/tag-text
---

# 内置标签插件 {#built-in-tags-plugin}

标签插件为页面添加了一级标签支持，通过使用标签对页面进行分类，增加了将相关页面分组并通过搜索和专 dedicateded 标签索引发现它们的可能性。如果您的文档很大，标签可以帮助您更快地发现相关信息。

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件扫描所有页面的[`tags`][meta.tags]元数据属性，并生成一个标签索引，这是一个倒排的标签列表和它们出现的页面。标签索引可以位于[`nav`][mkdocs.nav]的任何位置，为您的项目添加标签提供了最大的灵活性。

### 何时使用它 {#when-to-use-it}

如果您想在项目中添加一个或多个标签索引，标签插件是一个完美的选择，因为它使这个过程变得非常简单。此外，它与 Material for MkDocs 提供的几个其他[built-in plugins]完美集成：

<div class="grid cards" markdown>

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件使您的项目部分能够用[特定标签][meta.tags]进行注释，因此在添加页面时不会被遗忘。

    ---

    __简化不同部分中标签的组织和管理__

-   :material-newspaper-variant-outline: &nbsp; __[内置博客插件][blog]__

    ---

    标签插件允许将帖子与项目中的页面一起分类，以提高它们的可发现性并将帖子连接到您的文档。

    ---

    __您的文档的标签系统与您的博客集成__

</div>

  [meta]: meta.md
  [blog]: blog.md
  [built-in plugins]: index.md

## 配置 {#configuration}

<!-- md:version 8.2.0 -->
<!-- md:plugin [tags] – built-in -->
<!-- md:flag multiple -->

与所有[built-in plugins]一样，开始使用标签插件很简单。只需将以下行添加到`mkdocs.yml`中，然后开始使用[tags][meta.tags]对您的页面进行分类：

``` yaml
plugins:
  - tags
```

标签插件内置于 Material for MkDocs 中，无需安装。

  [tags]: tags.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.1.7 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - tags:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

### 标签 {#tags}

以下设置适用于标签：

---

#### <!-- md:setting config.tags -->

<!-- md:version 9.2.9 -->
<!-- md:default `true` -->

使用此设置启用或禁用渲染标签。插件仍然会从所有页面中提取标签，例如，用于[导出标签]而不渲染它们。可以使用以下方法禁用渲染：

``` yaml
plugins:
  - tags:
      tags: false
```

如果启用了[`export_only`][config.export_only]，此设置会自动禁用。

  [导出标签]: #export

---

#### <!-- md:setting config.tags_file -->

<!-- md:version 8.2.0 -->
<!-- md:default none -->

!!! info "在 [Insiders] 中不需要此设置"

    Insiders 提供了标签插件的 __彻底重写版本__，比社区版当前版本强大无数倍。它允许创建任意数量的标签索引（列表）、[有范围的列表]、[影子标签]、[嵌套标签]等等。

使用此设置指定标签索引的位置，该索引是用来渲染所有标签及其关联页面的列表。如果指定了此设置，标签将变为可点击，指向标签索引中的相应部分：

``` yaml
plugins:
  - tags:
      tags_file: tags.md
```

标签索引页面可以链接到`mkdocs.yml`的[`nav`][mkdocs.nav]部分的任何位置。不需要此设置——只有在您想要有一个标签索引时才使用它。

提供的路径从[`docs`目录][mkdocs.docs_dir]解析。

  [Insiders]: ../insiders/index.md
  [有范围的列表]: ../setup/setting-up-tags.md#scoped-listings
  [影子标签]: ../setup/setting-up-tags.md#shadow-tags
  [嵌套标签]: ../setup/setting-up-tags.md#nested-tags

---

#### <!-- md:setting config.tags_slugify -->

<!-- md:sponsors -->
<!-- md:version insiders-4.25.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改从帖子标题生成 URL 兼容 slugs 的函数。默认情况下，使用[Python Markdown 扩展]中的[`slugify`][pymdownx.slugs.slugify]函数，如下所示：

``` yaml
plugins:
  - tags:
      tags_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置对所有语言都具有 Unicode 支持，应该能产生良好的 slugs。当然，您也可以提供自定义的 slugification 函数以获得更细致的控制。

  [pymdownx.slugs.slugify]: https://github.com/facelessuser/pymdown-extensions/blob/01c91ce79c91304c22b4e3d7a9261accc931d707/pymdownx/slugs.py#L59-L65
  [Python Markdown 扩展]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

---

#### <!-- md:setting config.tags_slugify_separator -->

<!-- md:sponsors -->
<!-- md:version insiders-4.25.0 -->
<!-- md:default `-` -->

使用此设置更改传递给作为[`tags_slugify`][config.tags_slugify]一部分设置的 slugification 函数的分隔符。虽然默认是连字符，但可以设置为任何字符串，例如，`_`：

``` yaml
plugins:
  - tags:
      tags_slugify_separator: _
```

---

#### <!-- md:setting config.tags_slugify_format -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `tag:{slug}` -->

使用此设置更改生成标签 slugs 时使用的格式字符串。为标签 slugs 添加一个使其唯一的字符串前缀是个好主意，默认为：

``` yaml
plugins:
  - tags:
      tags_slugify_format: "tag:{slug}"
```

可用的占位符包括：

- `slug` – 标签 slug，使用[`tags_slugify`][config.tags_slugify]进行 slugify

---

#### <!-- md:setting config.tags_hierarchy -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->
<!-- md:flag experimental -->

使用此设置启用对标签层次结构的支持（嵌套标签，例如，`foo/bar`）。如果您打算创建标签的层次结构列表，您可以在`mkdocs.yml`中启用此设置：

``` yaml
plugins:
  - tags:
      tags_hierarchy: true
```

---

#### <!-- md:setting config.tags_hierarchy_separator -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `/` -->
<!-- md:flag experimental -->

使用此设置更改创建标签层次结构时使用的分隔符。默认情况下，标签由正斜杠`/`分隔，但您可以将其更改为任何字符串，例如，`.`：

``` yaml
plugins:
  - tags:
      tags_hierarchy_separator: .
```

---

#### <!-- md:setting config.tags_sort_by -->

<!-- md:sponsors -->
<!-- md:version insiders-4.26.2 -->
<!-- md:default `material.plugins.tags.tag_name` -->

使用此设置指定用于比较标签的自定义函数。默认情况下，标签比较区分大小写，但您可以使用`tag_name_casefold`进行不区分大小写的比较：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您还可以定义自己的比较函数，该函数必须返回表示标签的字符串或数字，用于排序，并在[`tags_sort_by`][config.tags_sort_by]中引用它。

---

#### <!-- md:setting config.tags_sort_reverse -->

<!-- md:sponsors -->
<!-- md:version insiders-4.26.2 -->
<!-- md:default `false` -->

使用此设置反转比较标签时标签排序的顺序。默认情况下，标签按升序排序，但您可以按以下方式反转排序：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### <!-- md:setting config.tags_name_property -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default [`tags`][meta.tags] -->

使用此设置更改插件使用的前 matter 属性的名称。通常不需要更改此设置，但如果您想更改，可以使用：

``` yaml
plugins:
  - tags:
      tags_name_property: tags
```

---

#### <!-- md:setting config.tags_name_variable -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `tags` -->

使用此设置更改插件使用的模板变量的名称。通常不需要更改此设置，但如果您想更改，可以使用：

``` yaml
plugins:
  - tags:
      tags_name_variable: tags
```

---

#### <!-- md:setting config.tags_allowed -->

<!-- md:sponsors -->
<!-- md:version insiders-4.25.0 -->
<!-- md:default none -->

插件允许根据预定义的标签列表检查标签，以捕获拼写错误或确保不会随意添加标签。使用以下方法指定您要允许的标签：

``` yaml
plugins:
  - tags:
      tags_allowed:
        - HTML5
        - JavaScript
        - CSS
```

如果页面引用了不在此列表中的标签，则插件会停止构建。可以使用[`tags`][meta.tags]元数据属性将页面分配给标签。

### 列表 {#listings}

以下设置可用于列表：

---

#### <!-- md:setting config.listings -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用列表。通常不需要更改此设置，因为列表完全通过内联注释创建，但如果需要，您可以禁用它们：

``` yaml
plugins:
  - tags:
      listings: false
```

如果启用了[`export_only`][config.export_only]，此设置会自动禁用。

  [导出标签]: #export

---

#### <!-- md:setting config.listings_map -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此定义列表配置，然后可以在列表中使用自定义标识符引用它。共享配置是个好主意，特别是当您有许多标签列表时：

``` yaml
plugins:
  - tags:
      listings_map:
        custom-id:
          scope: true
          exclude: Internal
```

然后，只需引用列表标识符：

``` html
<!-- material/tags custom-id -->
```

有关所有可用设置的列表，请参阅[列表部分]。

  [列表部分]: #listing_configuration

---

#### <!-- md:setting config.listings_sort_by -->

<!-- md:sponsors -->
<!-- md:version insiders-4.39.0 -->
<!-- md:default `material.plugins.tags.item_title` -->

使用此设置指定用于比较列表项的自定义函数。默认情况下，项目按标题排序，但您可以使用以下配置更改排序标准：

=== "按项目标题排序"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_title
    ```

=== "按项目 URL 排序"

    ``` yaml
    plugins:
      - tags:
          listings_sort_by: !!python/name:material.plugins.tags.item_url
    ```

您还可以定义自己的比较函数，该函数必须返回表示项的字符串或数字，用于排序，并在[`listings_sort_by`][config.listings_sort_by]中引用它。

---

#### <!-- md:setting config.listings_sort_reverse -->

<!-- md:sponsors -->
<!-- md:version insiders-4.39.0 -->
<!-- md:default `false` -->

使用此设置反转比较项时项目排序的顺序。默认情况下，项目按升序排序，但您可以按以下方式反转排序：

``` yaml
plugins:
  - tags:
      listings_sort_reverse: true
```

---

#### <!-- md:setting config.listings_tags_sort_by -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `material.plugins.tags.tag_name` -->

使用此设置指定用于比较列表中标签的自定义函数。默认情况下，标签比较区分大小写，但您可以使用`tag_name_casefold`进行不区分大小写：

``` yaml
plugins:
  - tags:
      tags_sort_by: !!python/name:material.plugins.tags.tag_name_casefold
```

您还可以定义自己的比较函数，该函数必须返回表示标签的字符串或数字，用于排序，并在[`tags_sort_by`][config.tags_sort_by]中引用它。

---

#### <!-- md:setting config.listings_tags_sort_reverse -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->

使用此设置反转比较标签时标签排序的顺序。默认情况下，标签按升序排序，但您可以按以下方式反转排序：

``` yaml
plugins:
  - tags:
      tags_sort_reverse: true
```

---

#### <!-- md:setting config.listings_directive -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `material/tags` -->

使用此设置更改插件在处理页面时查找的指令名称。如果您想使用比`material/tags`更短的指令，可以使用：

``` yaml
plugins:
  - tags:
      listings_directive: $tags
```

使用此设置后，列表必须按如下方式引用：

``` html
<!-- $tags { include: [foo, bar] } -->
```

---

#### <!-- md:setting config.listings_toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用在目录表中显示标签。如果您不希望标签显示在目录表中，可以禁用此行为：

``` yaml
plugins:
  - tags:
      listings_toc: false
```

### 影子标签 {#shadow-tags}

以下设置适用于影子标签：

---

#### <!-- md:setting config.shadow -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->

使用此设置指定插件是否应在[构建您的项目]时在页面和列表中包含影子标签，这可能对部署预览很有用：

=== "显示影子标签"

    ``` yaml
    plugins:
      - tags:
          shadow: true
    ```

=== "隐藏影子标签"

    ``` yaml
    plugins:
      - tags:
          shadow: false
    ```

---

#### <!-- md:setting config.shadow_on_serve -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应在[预览您的网站]时在页面和列表中包含影子标签。如果您不希望在预览时包含它们，请使用：

``` yaml
plugins:
  - tags:
      shadow_on_serve: false
```

  [预览您的网站]: ../creating-your-site.md#previewing-as-you-write

---

#### <!-- md:setting config.shadow_tags -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

插件允许指定预定义的影子标签列表，这些标签可以通过使用[`shadow`][config.shadow]设置包含或排除在构建中。必须将影子标签指定为列表：

``` yaml
plugins:
  - tags:
      shadow_tags:
        - Draft
        - Internal
```

---

#### <!-- md:setting config.shadow_tags_prefix -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定用于检查每个标签的前缀的字符串。如果标签以此字符串开头，则该标签被标记为影子标签。常见做法是使用`_`作为前缀：

``` yaml
plugins:
  - tags:
      shadow_tags_prefix: _
```

---

#### <!-- md:setting config.shadow_tags_suffix -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定用于检查每个标签的后缀的字符串。如果标签以此字符串结尾，则该标签被标记为影子标签。一个选项可以是使用`Internal`作为后缀：

``` yaml
plugins:
  - tags:
      shadow_tags_suffix: Internal
```

### 导出 {#export}

以下设置可用于导出：

---

#### <!-- md:setting config.export -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否在您的[`site`目录][mkdocs.site_dir]内创建一个`tags.json`文件，然后可以由其他插件和项目使用：

``` yaml
plugins:
  - tags:
      export: true
```

---

#### <!-- md:setting config.export_file -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `tags.json` -->

使用此设置更改存储导出标签的文件的路径。通常不需要更改此设置，但如果需要，请使用：

``` yaml
plugins:
  - tags:
      export_file: tags.json
```

提供的路径从[`site`目录][mkdocs.site_dir]解析。

---

#### <!-- md:setting config.export_only -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default `false` -->

此设置仅为方便提供，用于禁用标签和列表的渲染的单一设置（例如，使用环境变量），同时保持导出功能：

``` yaml
plugins:
  - tags:
      export_only: true
```

这将自动禁用[`tags`][config.tags]和[`listings`][config.listings]设置。

## 使用 {#usage}

### 元数据 {#metadata}

以下属性可用：

---

#### <!-- md:setting meta.tags -->

<!-- md:version 8.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将页面与一个或多个标签关联，使页面出现在生成的标签索引中。标签定义为字符串列表（允许使用空格）：

``` yaml
---
tags:
  - HTML5
  - JavaScript
  - CSS
---

# Page title
...
```

如果您想防止在将标签分配给页面时意外拼写错误，可以通过使用[`tags_allowed`][config.tags_allowed]设置在`mkdocs.yml`中设置预定义的允许标签列表。

### 列表配置 {#listing-configuration}

列表配置控制哪些标签包含在列表中或从列表中排除，以及列表是否仅包括当前范围内的页面。
此外，列表可以覆盖全局配置中的一些值。

以下设置可用：

---

#### <!-- md:setting listing.scope -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default `false` -->

此设置指定列表是否应仅考虑嵌入列表的页面的文档当前子部分内的页面：

=== "内联使用"

    ``` html
    <!-- material/tags { scope: true } -->
    ```

=== "在 `mkdocs.yml` 中使用"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              scope: false
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### <!-- md:setting listing.shadow -->

<!-- md:sponsors -->
<!-- md:version insiders-4.49.0 -->
<!-- md:default computed -->

此设置指定列表是否应包含影子标签，从而允许在每个列表的基础上覆盖全局[`shadow`][config.shadow]设置：

=== "内联使用"

    ``` html
    <!-- material/tags { shadow: true } -->
    ```

=== "在`mkdocs.yml`中使用"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              shadow: true
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### <!-- md:setting listing.toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default [`listings_toc`][config.listings_toc] -->

此设置指定列表是否应在目录表中呈现标签，从而允许在每个列表的基础上覆盖全局[`listings_toc`][config.listings_toc]设置：

=== "内联使用"

    ``` html
    <!-- material/tags { toc: true } -->
    ```

=== "在`mkdocs.yml`中使用"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              toc: true
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

---

#### <!-- md:setting listing.include -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定应包括在列表中的标签。每个具有此设置部分中标签的页面都将在相应的标签下列出：

=== "内联使用"

    ``` html
    <!-- material/tags { include: [foo, bar] } -->
    ```

=== "在 `mkdocs.yml` 中使用"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              include:
                - foo
                - bar
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

如果此设置为空，则包括所有标签和页面。

---

#### <!-- md:setting listing.exclude -->

<!-- md:sponsors -->
<!-- md:version insiders-4.48.0 -->
<!-- md:default none -->

使用此设置指定应从列表中排除的标签。每个具有此设置部分中标签的页面都将从列表中完全排除：

=== "内联使用"

    ``` html
    <!-- material/tags { exclude: [foo, bar] } -->
    ```

=== "在 `mkdocs.yml` 中使用"

    ``` yaml
    plugins:
      - tags:
          listings_map:
            custom-id:
              exclude:
                - foo
                - bar
    ```

    然后，只需引用列表标识符：

    ``` html
    <!-- material/tags custom-id -->
    ```

如果此设置为空，则不排除任何标签或页面。
