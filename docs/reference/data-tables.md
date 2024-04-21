---
icon: material/table-edit
---

# 数据表格 Data tables {#data-tables}

Material for MkDocs 为数据表格定义了默认样式——在项目文档中渲染表格数据的绝佳方式。此外，可以通过第三方库和一些[额外的 JavaScript]实现自定义，如[可排序表格]。

  [s可排序表格]: #sortable-tables
  [额外的 JavaScript]: ../customization.md#additional-javascript

## 配置 {#configuration}

此配置启用 Markdown 表格支持，通常应默认启用，但为确保，请添加以下行到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - tables
```

查看其他配置选项：

- [表格]

  [表格]: ../setup/extensions/python-markdown.md#tables

## 用法 {#usage}

数据表格可以在项目文档的任何位置使用，并且可以包含任意 Markdown，包括内联代码块以及[图标和表情]：

``` markdown title="Data table"
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |
```

<div class="result" markdown>

| 方法         | 描述                         |
| ----------- | ---------------------------- |
| `GET`       | :material-check:     获取资源 |
| `PUT`       | :material-check-all: 更新资源 |
| `DELETE`    | :material-close:     删除资源 |

</div>

  [图标和表情]: icons-emojis.md

### 列对齐 {#column-alignment}

如果您想要将特定列对齐到 `左`、`中` 或 `右`，您可以使用[常规 Markdown 语法]，在分隔符的开始和/或结束处放置 `:` 字符。

=== "Left"

    ``` markdown hl_lines="2" title="Data table, columns aligned to left"
    | Method      | Description                          |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | 方法       | 描述                             |
    | :---------- | :----------------------------------- |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

=== "Center"

    ``` markdown hl_lines="2" title="Data table, columns centered"
    | Method      | Description                          |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | 方法       | 描述                             |
    | :---------: | :----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

=== "Right"

    ``` markdown hl_lines="2" title="Data table, columns aligned to right"
    | Method      | Description                          |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     Fetch resource  |
    | `PUT`       | :material-check-all: Update resource |
    | `DELETE`    | :material-close:     Delete resource |
    ```

    <div class="result" markdown>

    | 方法       | 描述                             |
    | ----------: | -----------------------------------: |
    | `GET`       | :material-check:     获取资源        |
    | `PUT`       | :material-check-all: 更新资源        |
    | `DELETE`    | :material-close:     删除资源        |

    </div>

  [常规 Markdown 语法]: https://www.markdownguide.org/extended-syntax/#tables

## 自定义 {#customization}

### 可排序表格 {#sortable-tables}

如果您希望使数据表格可排序，可以添加 [tablesort]，它与 Material for MkDocs 原生集成，并将通过[额外的 JavaScript]与[即时加载]一起工作：

=== ":octicons-file-code-16: `docs/javascripts/tablesort.js`"

    ``` js
    document$.subscribe(function() {
      var tables = document.querySelectorAll("article table:not([class])")
      tables.forEach(function(table) {
        new Tablesort(table)
      })
    })
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - https://unpkg.com/tablesort@5.3.0/dist/tablesort.min.js
      - javascripts/tablesort.js
    ```

应用自定义后，可以通过点击列头对数据表格进行排序：

``` markdown title="Data table, columns sortable"
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |
```

<div class="result" markdown>

| 方法       | 描述                             |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     获取资源        |
| `PUT`       | :material-check-all: 更新资源        |
| `DELETE`    | :material-close:     删除资源        |

</div>

请注意，[tablesort] 提供了像数字、文件大小、日期和月份名称等不同的比较实现方式。更多信息请查看 [tablesort 文档][tablesort]。

<script src="https://unpkg.com/tablesort@5.3.0/dist/tablesort.min.js"></script>
<script>
  var tables = document.querySelectorAll("article table")
  new Tablesort(tables.item(tables.length - 1));
</script>

  [tablesort]: http://tristen.ca/tablesort/demo/
  [即时加载]: ../setup/setting-up-navigation.md#instant-loading

### 从文件导入表格 {#import-table-from-file}

插件 [mkdocs-table-reader-plugin][table-reader-docs] 允许您从 CSV 或 Excel 文件导入数据。

  [table-reader-docs]: https://timvink.github.io/mkdocs-table-reader-plugin/
