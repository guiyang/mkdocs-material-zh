---
icon: material/tooltip-plus
---

# 工具提示 Tooltips

技术文档经常使用许多缩写词，这些缩写词可能需要额外的解释，特别是对于项目的新用户。对于这些问题，MkDocs 的 Material 使用 Markdown 扩展的组合来启用全站词汇表。

## 配置

此配置启用缩写并允许构建一个简单的项目范围内的词汇表，从中央位置获取定义。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - abbr
  - attr_list
  - pymdownx.snippets
```

查看更多配置选项：

- [缩写]
- [属性列表]
- [片段]

  [缩写]: ../setup/extensions/python-markdown.md#abbreviations
  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [片段]: ../setup/extensions/python-markdown-extensions.md#snippets

### 改进的工具提示

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

启用改进的工具提示后，MkDocs 的 Material 将替换浏览器的 `title` 属性渲染逻辑，使用美观的小工具提示。将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - content.tooltips
```

现在，以下元素将渲染工具提示：

- __内容__ – 带有 `title` 的元素、永久链接和代码复制按钮
- __头部__ – 首页按钮、头部标题、颜色调板切换和仓库链接
- __导航__ – 用省略号缩短的链接，即 `...`

## 使用

### 添加工具提示

[Markdown 语法] 允许为每个链接指定一个 `title`，当启用 [改进的工具提示] 时，将呈现为一个美观的工具提示。使用以下行为链接添加工具提示：

``` markdown title="Link with tooltip, inline syntax"
[悬停我](https://example.com "我是一个工具提示！")
```

<div class="result" markdown>

[悬停我](https://example.com "我是一个工具提示！")

</div>

工具提示也可以添加到链接引用：

``` markdown title="Link with tooltip, reference syntax"
[悬停我][示例]

  [示例]: https://example.com "I'm a tooltip!"
```

<div class="result" markdown>

[悬停我](https://example.com "我是一个工具提示！")

</div>

对于所有其他元素，可以使用 [属性列表] 扩展添加 `title`：

``` markdown title="Icon with tooltip"
:material-information-outline:{ title="Important information" }
```

<div class="result" markdown>

:material-information-outline:{ title="Important information" }

</div>

  [Markdown 语法]: https://daringfireball.net/projects/markdown/syntax#link
  [改进的工具提示]: #improved-tooltips

### 添加缩写

可以使用类似于网址和 [脚注] 的特殊语法定义缩写，以 `*` 开始并紧随其后的方括号中包含要关联的术语或缩写：

``` markdown title="Text with abbreviations"
HTML 规范由 W3C 维护。

*[HTML]: 超文本标记语言
*[W3C]: 万维网联盟
```

<div class="result" markdown>

HTML 规范由 W3C 维护。

*[HTML]: 超文本标记语言
*[W3C]: 万维网联盟

</div>

  [脚注]: footnotes.md

### 添加词汇表

可以使用 [片段] 扩展实现一个简单的词汇表，通过将所有缩写移动到一个专用文件[^1]，并通过以下配置将此文件 [自动追加] 到所有页面：

  [^1]:
    强烈建议将包含缩写的 Markdown 文件放在 `docs` 文件夹外部（此处使用名为 `includes` 的文件夹），因为 MkDocs 可能会因未引用的文件而发出警告。

=== ":octicons-file-code-16: `includes/abbreviations.md`"

    ```` markdown
    *[HTML]: 超文本标记语言
    *[W3C]: 万维网联盟
    ````

=== ":octicons-file-code-16: `mkdocs.yml`"

    ```` yaml
    markdown_extensions:
      - pymdownx.snippets:
          auto_append:
            - includes/abbreviations.md
    ````

  [自动追加]: https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#auto-append-snippets

!!! tip

    使用位于 `docs` 文件夹外的专用文件时，将父目录添加到 `watch` 文件夹列表中，以便在更新词汇表文件时，项目在运行 `mkdocs serve` 时自动重新加载。

    ```` yaml
    watch:
      - includes
    ````
