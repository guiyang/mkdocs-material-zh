# 设置页头 {#setting-up-the-header}

Material for MkDocs 的页头可以定制显示一个公告栏，该公告栏在滚动时消失，并提供一些进一步配置的选项。它还包括 [搜索栏] 和一个展示你的项目的 [git 仓库] 的位置，这些在专门的指南中有所说明。

  [搜索栏]: setting-up-site-search.md
  [git 仓库]: adding-a-git-repository.md

## 配置 {#configuration}

### 自动隐藏 {#automatic-hiding}

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用自动隐藏后，当用户滚动超过某个阈值时，页头将自动隐藏，为内容留出更多空间。将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - header.autohide
```

### 公告栏 {#announcement-bar}

<!-- md:version 5.0.0 -->
<!-- md:flag customization -->

Material for MkDocs 包含一个公告栏，这是展示项目新闻或其他重要信息给用户的完美位置。当用户滚动过页头时，公告栏将自动消失。为了添加一个公告栏，[扩展主题]并[覆盖 `announce` 块][overriding blocks]，该块默认为空：

``` html
{% extends "base.html" %}

{% block announce %}
  <!-- Add announcement here, including arbitrary HTML -->
{% endblock %}
```

  [扩展主题]: ../customization.md#extending-the-theme
  [overriding blocks]: ../customization.md#overriding-blocks

#### 标记为已读 {#mark-as-read}

<!-- md:version 8.4.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

为了渲染可以由用户标记为已读的临时公告，可以包括一个用于关闭当前公告的按钮。将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - announce.dismiss
```

当用户点击按钮时，当前公告被关闭并不再显示，直到公告内容发生变化。这一切都是自动处理的。

[滚动到本页顶部][top]查看实际操作。

  [top]: #
