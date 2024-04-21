# 构建离线使用的文档 {#building-for-offline-usage}

如果您希望将文档与产品一起交付，MkDocs 提供了支持——通过主题支持，[MkDocs] 允许构建可离线使用的文档。值得注意的是，Material for MkDocs 为其许多功能提供了离线支持。

  [MkDocs]: https://www.mkdocs.org

## 配置 {#configuration}

### 内置离线插件 {#built-in-offline-plugin}

<!-- md:version 9.0.0 -->
<!-- md:plugin [offline] – built-in -->

内置离线插件确保当您将[站点目录]的内容作为下载分发时，[站点搜索]能够工作。只需在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - offline
```

有关所有设置的列表，请查阅[插件文档]。

  [offline]: ../plugins/offline.md
  [插件文档]: ../plugins/offline.md

!!! tip "自动捆绑所有外部资源"

    [内置隐私插件] 使使用外部资源构建离线使用的文档变得简单，因为它会自动下载所有外部资源，以便与您的文档一起分发。

  [站点搜索]: setting-up-site-search.md
  [站点目录]: https://www.mkdocs.org/user-guide/configuration/#site_dir
  [内置隐私插件]:../plugins/privacy.md

#### 限制 {#limitations}

Material for MkDocs 提供了许多交互功能，其中一些由于现代浏览器的限制将无法从文件系统中工作：所有使用 `fetch` API 的功能都将出错。

因此，在为离线使用构建时，请确保禁用以下配置设置：[即时加载]、[站点分析]、[Git 仓库]、[版本控制]和[评论系统]。

  [即时加载]: setting-up-navigation.md#instant-loading
  [站点分析]: setting-up-site-analytics.md
  [版本控制]: setting-up-versioning.md
  [Git 仓库]: adding-a-git-repository.md
  [评论系统]: adding-a-comment-system.md
