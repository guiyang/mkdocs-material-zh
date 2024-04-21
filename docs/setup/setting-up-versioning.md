# 设置版本控制 {#setting-up-versioning}

Material for MkDocs 通过与外部工具集成，使部署项目文档的多个版本变得简单，这些工具为 MkDocs 添加了这些功能，即 [mike]。当部署新版本时，旧版本的文档保持不变。

  [mike]: https://github.com/jimporter/mike

## 配置 {#configuration}

### 版本控制 {#versioning}

<!-- md:version 7.0.0 -->
<!-- md:utility [mike] -->

[mike] 使部署项目文档的多个版本变得简单。它与 Material for MkDocs 原生集成，并可以通过 `mkdocs.yml` 启用：

``` yaml
extra:
  version:
    provider: mike
```

这将在页头渲染一个版本选择器：

<figure markdown>

[![Version selector preview]][Version selector preview]

  <figcaption markdown>

查看版本控制示例，看看它的实际操作 - [squidfunk.github.io/mkdocs-material-example-versioning][version example]

  </figcaption>
</figure>

!!! quote "[为什么使用 mike?]"

    mike 围绕这样一个理念构建：一旦你为特定版本生成了文档，你就再也不需要触摸那个版本了。这意味着你永远不必担心 MkDocs 中的破坏性更改，因为你的旧文档（用旧版本的 MkDocs 构建）已经生成，并存在于你的 `gh-pages` 分支中。

    虽然 mike 很灵活，但它围绕将你的文档放在 `<major>.<minor>` 目录中进行了优化，还可以为特别重要的版本设置可选别名（例如 `latest` 或 `dev`）。这使得创建到你想指向的文档版本的永久链接变得容易。

  [Version selector preview]: ../assets/screenshots/versioning.png
  [version example]: https://squidfunk.github.io/mkdocs-material-example-versioning/
  [为什么使用 mike?]: https://github.com/jimporter/mike#why-use-mike

### 切换版本时停留在同一页面 {#stay-on-the-same-page-when-switching-versions}

当用户在版本选择器中选择一个版本时，他们通常希望转到他们之前正在查看的页面对应的页面。Material for MkDocs 默认实现了这种行为，但有几个注意事项：

- [`site_url`] 必须在 `mkdocs.yml` 中正确设置。请参阅["发布新版本"](#publishing-a-new-version)部分中的示例。
- 你必须在该 URL（而不是本地，例如）下查看站点。
- 重定向通过 JavaScript 发生，你无法提前知道你将被重定向到哪个页面。

[`site_url`]: https://www.mkdocs.org/user-guide/configuration/#site_url

### 版本警告 {#version-warning}

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

如果你使用版本控制，你可能希望在用户访问非最新版本时显示警告。使用[主题扩展]，你可以[覆盖 `outdated` 块][overriding blocks]：

``` html
{% extends "base.html" %}

{% block outdated %}
  You're not viewing the latest version.
  <a href="{{ '../' ~ base_url }}"> <!-- (1)! -->
    <strong>Click here to go to latest.</strong>
  </a>
{% endblock %}
```

1.  给定这个 `href` 属性值，链接将始终重定向到你的站点的根，然后重定向到最新版本。这确保旧版本的站点不依赖于特定别名，例如 `latest`，允许以后更改别名而不破坏早期版本。

这将在页头上方渲染一个版本警告：

[![Version warning preview]][Version warning preview]

默认版本由 `latest` 别名标识。如果你希望将另一个别名设置为最新版本，例如 `stable`，添加以下行到 `mkdocs.yml`：

``` yaml
extra:
  version:
    default: stable # (1)!
```

1.  你还可以定义多个别名作为默认版本，例如 `stable` 和 `development`。

    ``` yaml
    extra:
      version:
        default:
          - stable
          - development
    ```

    现在，拥有 `stable` 和 `development` 别名的每个版本都不会显示版本警告。

确保一个别名与[默认版本]匹配，因为这是用户被重定向的地方。

  [主题扩展]: ../customization.md#extending-the-theme
  [overriding blocks]: ../customization.md#overriding-blocks
  [Version warning preview]: ../assets/screenshots/version-warning.png
  [默认版本]: #setting-a-default-version

## 使用 {#usage}

虽然本节概述了发布新版本的基本工作流程，最好查看[mike 的文档][mike]，以使自己熟悉其机制。

### 发布新版本 {#publishing-a-new-version}

如果你想发布项目文档的新版本，请选择一个版本标识符并更新设置为默认版本的别名：

```
mike deploy --push --update-aliases 0.1 latest
```

注意，每个版本都将作为你的 `site_url` 的子目录部署，你应该明确设置。例如，如果你的 `mkdocs.yml` 包含：

``` yaml
site_url: 'https://docs.example.com/'  # Trailing slash is recommended
```

文档将发布到如下 URL：

- _docs.example.com/0.1/_
- _docs.example.com/0.2/_
- ...

### 设置默认版本 {#setting-a-default-version}

从 [mike] 开始，设置一个别名作为默认版本是个好主意，例如 `latest`，并且在发布新版本时，始终更新别名以指向最新版本：

```
mike set-default --push latest
```

发布新版本时，[mike] 将在你的项目文档的根部创建一个重定向到与别名相关联的版本的重定向：

_docs.example.com_ :octicons-arrow-right-24: _docs.example.com/0.1_
