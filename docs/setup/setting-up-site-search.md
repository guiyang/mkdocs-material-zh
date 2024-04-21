---
search:
  boost: 1.05
---

# 设置站点搜索 {#setting-up-site-search}

Material for MkDocs 提供了一种出色的客户端搜索实现，无需集成第三方服务，可能不符合隐私法规。此外，搜索甚至可以 [离线] 使用，允许用户下载您的文档。

  [离线]: building-for-offline-usage.md

## 配置 {#configuration}

### 内置搜索插件 {#built-in-search-plugin}

<!-- md:version 0.1.0 -->
<!-- md:plugin -->

内置搜索插件与 Material for MkDocs 无缝集成，增加了支持多语言的客户端搜索，使用 [lunr] 和 [lunr-languages]。它默认启用，但在使用其他插件时必须重新添加到 `mkdocs.yml`：

``` yaml
plugins:
  - search
```

有关所有设置的列表，请参阅 [插件文档]。

  [插件文档]: ../plugins/search.md

  [lunr]: https://lunrjs.com
  [lunr-languages]: https://github.com/MihaiValentin/lunr-languages

### 搜索建议 {#search-suggestions}

<!-- md:version 7.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用搜索建议后，搜索将显示最后一个词的最可能完成情况，可以通过 ++arrow-right++ 键接受。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - search.suggest
```

搜索 [:octicons-search-24: search su][搜索建议示例] 会显示 ^^搜索建议^^。

  [搜索建议示例]: ?q=search+su

### 搜索高亮 {#search-highlighting}

<!-- md:version 7.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用搜索高亮时，用户点击搜索结果后，Material for MkDocs 将高亮显示所有链接后的出现次数。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - search.highlight
```

搜索 [:octicons-search-24: code blocks][搜索高亮示例] 将高亮显示两个术语的所有出现。

  [Search highlighting example]: ../reference/code-blocks.md?h=code+blocks

### 搜索共享 {#search-sharing}

<!-- md:version 7.2.0 -->
<!-- md:feature -->

当激活搜索共享时，会在重置按钮旁边渲染一个 :material-share-variant: 分享按钮，允许深度链接到当前的搜索查询和结果。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - search.share
```

当用户点击分享按钮时，URL 会自动复制到剪贴板。

## 使用 {#usage}

### 搜索提升 {#search-boosting}

<!-- md:version 8.3.0 -->
<!-- md:flag metadata -->

可以通过 Markdown 文件顶部的前 matter `search.boost` 属性提升页面在搜索中的排名，使其排名更高。在 Markdown 文件的顶部添加以下行：

=== ":material-arrow-up-circle: 提升排名"

    ``` yaml
    ---
    search:
      boost: 2 # (1)!
    ---

    # Page title
    ...
    ```

    1.  :woman_in_lotus_position: 提升页面时，请温和地从 __低值__ 开始。

=== ":material-arrow-down-circle: 降低排名"

    ``` yaml
    ---
    search:
      boost: 0.5
    ---

    # Page title
    ...
    ```

### 搜索排除 {#search-exclusion}

<!-- md:version 9.0.0 -->
<!-- md:flag metadata -->
<!-- md:flag experimental -->

可以通过 Markdown 文件顶部的前 matter `search.exclude` 属性从搜索中排除页面，将其从索引中移除。在 Markdown 文件的顶部添加以下行：

``` yaml
---
search:
  exclude: true
---

# Page title
...
```

#### 排除段（sections） {#excluding-sections}

启用 [属性列表] 时，可以通过在 Markdown 标题后添加 `data-search-exclude` 指令来从搜索中排除特定页面部分：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # Page title

    ## Section 1

    The content of this section is included

    ## Section 2 { data-search-exclude }

    The content of this section is excluded
    ```

=== ":octicons-codescan-16: `search_index.json`"

    ``` json
    {
      ...
      "docs": [
        {
          "location":"page/",
          "text":"",
          "title":"Document title"
        },
        {
          "location":"page/#section-1",
          "text":"<p>The content of this section is included</p>",
          "title":"Section 1"
        }
      ]
    }
    ```

  [属性列表]: extensions/python-markdown.md#attribute-lists

#### 排除块 (blocks) {#excluding-blocks}

启用 [属性列表] 时，可以通过在 Markdown 内联或块级元素后添加 `data-search-exclude` 指令来从搜索中排除特定部分：

=== ":octicons-file-code-16: `docs/page.md`"

    ``` markdown
    # Page title

    The content of this block is included

    The content of this block is excluded
    { data-search-exclude }
    ```

=== ":octicons-codescan-16: `search_index.json`"

    ``` json
    {
      ...
      "docs": [
        {
          "location":"page/",
          "text":"<p>The content of this block is included</p>",
          "title":"Document title"
        }
      ]
    }
    ```
