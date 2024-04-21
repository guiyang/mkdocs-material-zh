---
title: 内置分组插件
icon: material/format-list-group
---

# 内置分组插件 {#built-in-group-plugin}

分组插件允许将插件分组为逻辑单元，以便使用[环境变量][mkdocs.env]为特定环境有条件地启用或禁用它们，例如，在持续集成（CI）期间[构建您的站点]时仅启用一部分插件。

  [构建您的站点]: ../creating-your-site.md#building-your-site

## 目标 {#objective}

### 工作原理 {#how-it-works}

仅当启用组时，插件才有条件且延迟加载组内的所有插件，这意味着当组被禁用时，插件不会增加任何开销。这也意味着，只有在启用组时才需要安装组内的插件。

组内的插件按照它们在[`plugins`][mkdocs.plugins]列表中顶层定义的顺序执行。因此，顺序得以保留且确定性。

### 何时使用 {#when-to-use-it}

每当您在特定环境中只需要使用多个插件时，例如，在持续集成（CI）期间构建您的项目时，该插件是简化配置的完美工具，因为它无需将配置拆分为多个文件。

它可以与任何内置或第三方插件一起使用。

## 配置 {#configuration}

<!-- md:version 9.3.0 -->
<!-- md:plugin [group] – built-in -->
<!-- md:flag multiple -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用分组插件很简单。只需在`mkdocs.yml`中添加以下几行，并开始将插件分割成逻辑单元：

``` yaml
plugins:
  - group
```

分组插件内置于Material for MkDocs中，无需安装。

  [group]: group.md
  [内置插件]: index.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.3.0 -->
<!-- md:default `false` -->

使用此设置在[构建您的项目]时启用或禁用插件。该插件与所有其他内置插件的行为不同 -- __默认情况下它是禁用的__。要启用一个组，请使用：

``` yaml
plugins:
  - group:
      enabled: !ENV CI # (1)!
```

1.  如果您只想出于更好的组织而使用分组插件，并且总是希望启用其中的插件，请使用：

    ``` yaml
    plugins:
      - group:
          enabled: true
    ```

默认情况下禁用插件的决定是为了简化环境变量的使用，因为它消除了为环境变量提供默认值的需要。

现在，在[构建您的项目]时，您可以通过设置[环境变量][mkdocs.env]来启用一个组：

``` sh
CI=true mkdocs build
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

---

#### <!-- md:setting config.plugins -->

<!-- md:version 9.3.0 -->
<!-- md:default none -->

使用此设置列出组内的插件。语法与[`plugins`][mkdocs.plugins]设置完全相同，因此您可以简单地复制您想要分组的插件列表，例如：

``` yaml
plugins:
  - group:
      plugins:
        - optimize
        - minify
```

这里提到的插件仅用于说明目的。
