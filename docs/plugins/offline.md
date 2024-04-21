---
title: 内置离线插件
icon: material/connection
---

# 内置离线插件 {#built-in-offline-plugin}

[MkDocs][mkdocs] 是少数几个允许构建可离线查看的文档框架之一，用户无需服务器即可直接查看。通过离线插件，您可以将 [`site` 目录][mkdocs.site_dir] 分发为可下载的 `.zip` 文件，同时保留大部分交互功能。

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

在[构建您的项目]后，切换到[`site`目录][mkdocs.site_dir]并在浏览器中打开 `index.html` —— 您现在正在从本地文件系统查看您的文档！大多数浏览器会在地址栏显示 `file://` 来表示这一点。但是，您会发现站点搜索已经消失了。

Material for MkDocs 提供许多交互功能，其中一些由于现代浏览器的限制在本地文件系统中无法工作。更具体和技术性地说，所有对 [Fetch API] 的调用都会出现错误消息：

```
Cross origin requests are only supported for protocol schemes: http, [...]
```

由于安全原因，浏览器施加了这些限制，这降低了您项目的交互性。离线插件确保通过将搜索索引移至 JavaScript 文件，并利用 @squidfunk 的 [iframe-worker] 仿真器，使站点搜索继续工作。

此外，该插件自动禁用 [`use_directory_urls`][mkdocs.use_directory_urls] 设置，确保用户可以直接从本地文件系统打开您的文档。

有一些 [限制]。

  [构建您的项目]: ../creating-your-site.md#building-your-site
  [Fetch API]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
  [iframe-worker]: https://github.com/squidfunk/iframe-worker
  [限制]: #limitations


### 何时使用它 {#when-to-use-it}

正如名称已经表明的那样，当您为离线分发[构建您的项目]时应该使用该插件。同样重要的是要知道，离线插件与以下其他插件协同工作良好，帮助创建更好的可离线文档：

<div class="grid cards" markdown>

-   :material-shield-account: &nbsp; __[内置隐私插件][privacy]__

    ---

    隐私插件使在为离线使用构建时使用外部资源变得简单，因为它会自动下载这些资源，以便与您的文档一起分发。

    ---

    __您的文档可以在没有互联网连接的情况下工作[^1]__

-   :material-rabbit: &nbsp; __[内置优化插件][optimize]__

    ---

    优化插件自动识别并优化您的项目中引用的所有媒体文件，使用压缩和转换技术。

    ---

    __您的文档可以作为更小的 `.zip` 文件分发__

</div>

  [^1]:
    您可能想知道为什么在使用离线插件构建真正的可离线文档时，[隐私插件][privacy] 是必要的。虽然在离线插件中也可以添加支持下载外部资源的功能，但这项功能已在隐私插件中完全实现，这正是其存在的真正原因。

    Material for MkDocs 采用模块化方法进行插件系统的构建——许多插件可以完美协同工作并增强彼此的功能，允许通过几行配置解决复杂问题。

  [privacy]: privacy.md
  [optimize]: optimize.md

## 配置 {#configuration}

<!-- md:version 9.0.0 -->
<!-- md:plugin [offline] – built-in -->

与所有[内置插件]一样，开始使用离线插件非常简单。只需将以下行添加到 `mkdocs.yml`，并开始构建可离线的文档：

``` yaml
plugins:
  - offline
```

离线插件已内置于 Material for MkDocs 中，无需安装。

  [offline]: offline.md
  [内置插件]: index.md

### 通用 {#General}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.0.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。如果您想同时构建在线和离线的文档，使用[环境变量][mkdocs.env]是个好主意：

``` yaml
plugins:
  - offline:
      enabled: !ENV [OFFLINE, false]
```

## 限制 {#limitations}

启用离线插件时，请确保禁用以下设置，因为它们使用 [Fetch API]，当从本地文件系统调用时会出现错误：

- [即时加载][Instant loading]
- [站点分析][Site analytics]
- [版本控制][Versioning]
- [评论系统][Comment systems]

  [Instant loading]: ../setup/setting-up-navigation.md#instant-loading
  [Site analytics]: ../setup/setting-up-site-analytics.md
  [Versioning]: ../setup/setting-up-versioning.md
  [Comment systems]: ../setup/adding-a-comment-system.md
