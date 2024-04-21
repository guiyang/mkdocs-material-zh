---
title: 内置信息插件
icon: material/information
---

# Built-in info plugin

信息插件是一个专门用于创建独立的 [最小化复现] 作为 `.zip` 文件的实用工具，当 [报告缺陷] 或提出 [更改请求] 时，使我们维护者与您的沟通变得更加容易，因为我们有一个共同的基础来合作。

  [最小化复现]: ../guides/creating-a-reproduction.md
  [报告缺陷]: ../contributing/reporting-a-bug.md
  [更改请求]: ../contributing/requesting-a-change.md

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件通过收集有关您项目的环境和配置的必要信息，帮助您准备一个最小化复现。这使我们更容易修复错误，因为它要求您[升级到最新版本]并[移除您的自定义设置]。

遵循这些原则，您可以确信您不会报告一个在后续发布中已经修复的错误，或者由您的某些自定义设置所导致的错误。更重要的是，您积极帮助我们尽可能快地修复错误。

插件的输出是一个`.zip`文件，您可以与我们维护者共享。

  [升级到最新版本]: ../contributing/reporting-a-bug.md#upgrade-to-latest-version
  [移除您的自定义设置]: ../contributing/reporting-a-bug.md#remove-customizations


### 何时使用它 {#when-to-use-it}

每当您[报告一个错误][报告缺陷]或有一些要讨论的事情，如一个问题或[更改请求][更改请求]，您都应该附上一个小的、独立的最小化复现。可运行的示例有助于使沟通更有效率，给我们维护者更多时间来推动项目向前发展。对于错误报告，最小化复现是必须的

## 配置 {#configuration}

<!-- md:version 9.0.0 -->
<!-- md:plugin [info] – built-in -->

要开始使用内置信息插件，只需添加以下行到`mkdocs.yml`，并快速[创建一个最小化复现]与我们维护者共享：

``` yaml
plugins:
  - info
```

信息插件内置于Material for MkDocs中，无需安装。

  [info]: info.md
  [创建一个最小化复现]: ../guides/creating-a-reproduction.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.0.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。通常不需要指定此设置，但如果您想要禁用插件，请使用：

``` yaml
plugins:
  - info:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

---

#### <!-- md:setting config.enabled_on_serve -->

<!-- md:version 9.0.6 -->
<!-- md:default `false` -->

使用此设置控制在[预览您的网站]时是否应启用插件。通常不需要指定此设置，但如果您想更改此行为，请使用：

``` yaml
plugins:
  - info:
      enabled_on_serve: true
```

此设置简化了创建和检查最小化复现的过程，因为它允许在不必先禁用插件的情况下快速迭代复现。

  [预览您的网站]: ../creating-your-site.md#previewing-as-you-write

### 归档 {#archive}

---

#### <!-- md:setting config.archive -->

<!-- md:version 9.0.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应从项目创建`.zip`文件或在版本检查后退出。此设置仅用于调试插件本身：

``` yaml
plugins:
  - info:
      archive: false
```

---

#### <!-- md:setting config.archive_stop_on_violation -->

<!-- md:version 9.0.0 -->
<!-- md:default `true` -->

使用此设置控制插件在未满足[要求]时是否应停止创建`.zip`文件。此设置只能在[报告错误][报告缺陷]时使用，该错误与我们文档中[明确提到的自定义]相关。您可以更改它：

``` yaml
plugins:
  - info:
      archive_stop_on_violation: false
```

如果您在[报告一个错误][报告缺陷]时使用此设置，请解释为什么认为包含自定义设置是必要的。如果您不确定，请先通过[创建讨论]向我们咨询。

  [要求]: #how-it-works
  [明确提到的自定义]: ?q=%22extends+base%22
  [创建讨论]: https://github.com/squidfunk/mkdocs-material/discussions
