---
title: 内置排版插件
icon: material/format-title
---

# 内置排版插件 {#built-in-typeset-plugin}

排版插件允许在导航和目录表中保留标题和标题的丰富展示。这意味着代码块、图标、表情符号以及任何其他内联格式化都可以按照页面内容中定义的方式精确渲染。

---

<!-- md:sponsors --> __仅限赞助者__ —— 此插件目前仅对[我们的赞助者]开放。

  [我们的赞助者]: ../insiders/index.md


## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

在[构建您的项目]时，MkDocs 从标题中提取纯文本并丢弃原始格式化。通常，这是有用的，也是个好主意，因为这些信息可以提供给其他可能在传递 HTML 而不是纯文本时遇到问题的插件。

然而，这也意味着所有格式化都丢失了。

插件挂接到渲染过程中，提取原始标题，并使它们可用于模板和插件。Material for MkDocs 的模板使用这些信息来渲染导航和目录表的丰富版本。

  [构建您的项目]: ../creating-your-site.md#building-your-site

### 何时使用它 {#when-to-use-it}

通常建议使用此插件，因为它是一个即插即用的解决方案，不需要任何配置，并且设计为开箱即用。由于它不会覆盖而只是添加信息，因此预期不会与其他插件冲突。

## 配置 {#configuration}

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:plugin [typeset] – built-in -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用排版插件非常简单。只需将以下行添加到`mkdocs.yml`中，然后观察丰富的导航和目录表：

``` yaml
plugins:
  - typeset
```

排版插件内置于 Material for MkDocs 中，无需安装。

  [typeset]: typeset.md
  [内置插件]: index.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.27.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - typeset:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site
