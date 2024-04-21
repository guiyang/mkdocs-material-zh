---
title: 内置元数据插件
icon: material/file-tree
---

# 内置元数据插件 {#built-in-meta-plugin}

元数据插件解决了为文件夹中的所有页面（即您项目的一个子部分）设置元数据（前言）的问题，这对于确保某些页面子集具有特定标签、使用自定义模板或归属于某个作者特别有用。

---

<!-- md:sponsors --> __仅限赞助者__ — 此插件目前仅供[我们的优秀赞助者]使用。

  [我们的优秀赞助者]: ../insiders/index.md

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件扫描[`docs`目录][mkdocs.docs_dir]中的`.meta.yml`文件，并递归地将这些文件的内容与同一文件夹及所有子文件夹中包含的所有页面的元数据（前言）合并。例如，如果您想向多个页面添加标签 <span class="md-tag">示例</span>，请使用：

``` yaml title=".meta.yml"
tags:
  - Example
```

现在，根据以下目录布局，如果您将文件存储在名为`example`的文件夹中，则该文件夹中的所有页面都会接收到标签，而文件夹外的所有页面则不受影响：

``` { .sh .no-copy hl_lines="4-8" }
.
├─ docs/
│  ├─ ...
│  ├─ example/
│  │  ├─ .meta.yml
│  │  ├─ a.md
│  │  ├─ ...
│  │  └─ z.md
│  └─ ...
└─ mkdocs.yml
```

在合并元数据时，列表和字典会递归合并，这意味着您可以向列表中追加值，并在字典中的任意级别上添加或设置特定属性。

### 何时使用它 {#when-to-use-it}

虽然插件本身除了添加和合并元数据外并没有提供太多功能，但它是许多其他内置插件的完美伴侣，这些插件是Material for MkDocs提供的。元数据插件与其他内置插件的一些最强大组合包括：

<div class="grid cards" markdown>

-   :material-share-circle: &nbsp; __[内置社交插件][social]__

    ---

    元数据插件可用于[更改布局]以用于社交卡片或[更改特定布局选项]，例如[背景]或[颜色]，以适用于页面的子集。

    ``` yaml title=".meta.yml"
    social:
      cards_layout: default/variant
    ```

-   :material-newspaper-variant-outline: &nbsp; __[内置博客插件][blog]__

    ---

    元数据插件允许自动将博客帖子与特定[作者]和[类别]关联，确保博客帖子始终正确注释。

    ``` yaml title=".meta.yml"
    authors:
      - squidfunk
    ```

-   :material-tag-text: &nbsp; __[内置标签插件][tags]__

    ---

    元数据插件使得确保您的项目的子部分用[特定标签]注释成为可能，这样在添加页面时就不会忘记。

    ``` yaml title=".meta.yml"
    tags:
      - Example
    ```

-   :material-magnify: &nbsp; __[内置搜索插件][search]__

    ---

    元数据插件使得在搜索结果中[提升]特定部分或完全[排除]它们被索引变得简单，从而提供更细致的搜索控制。

    ``` yaml title=".meta.yml"
    search:
      exclude: true
    ```

</div>

  [social]: social.md
  [更改布局]: social.md#meta.social.cards_layout
  [更改特定布局选项]: social.md#meta.social.cards_layout_options
  [背景]: social.md#option.background_color
  [颜色]: social.md#option.color
  [blog]: blog.md
  [作者]: blog.md#meta.authors
  [类别]: blog.md#meta.categories
  [tags]: tags.md
  [特定标签]: tags.md#meta.tags
  [search]: search.md
  [排除]: search.md#meta.search.exclude
  [提升]: search.md#meta.search.boost

## 配置 {#configuration}

<!-- md:sponsors -->
<!-- md:version insiders-4.21.0 -->
<!-- md:plugin [meta] – built-in -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用元数据插件非常简单。只需将以下行添加到`mkdocs.yml`，并开始一次性应用多个页面的元数据：

``` yaml
plugins:
  - meta
```

元数据插件已包含在Material for MkDocs中，无需安装。

  [meta]: meta.md
  [内置插件]: index.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。通常不需要指定此设置，但如果您想要禁用插件，请使用：

``` yaml
plugins:
  - meta:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

### 元文件 {#meta-file}

以下设置适用于元文件：

---

#### <!-- md:setting config.meta_file -->

<!-- md:sponsors -->
<!-- md:version insiders-4.21.0 -->
<!-- md:default `.meta.yml` -->

使用此设置更改插件在扫描[`docs`目录][mkdocs.docs_dir]时寻找的元文件名称。通常不需要更改此设置，但如果您想更改它，请使用：

``` yaml
plugins:
  - meta:
      meta_file: .meta.yml
```

提供的路径从[`docs`目录][mkdocs.docs_dir]递归解析。
