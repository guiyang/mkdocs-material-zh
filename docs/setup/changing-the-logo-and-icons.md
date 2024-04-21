# 更改徽标和图标 {#changing-the-logo-and-icons}

安装 Material for MkDocs 后，您将立即获得_超过 8,000 个图标_，可用于自定义主题的特定部分和/或在 Markdown 中编写文档时使用。还不够？您还可以通过最小的努力添加[额外图标]。

  [额外图标]: #additional-icons

## 配置 {#configuration}

### 徽标 {#logo}

<!-- md:version 0.1.0 -->
<!-- md:default `material/library` -->

徽标可以更改为位于 `docs` 文件夹中的用户提供的图片（任何类型，包括 `*.png` 和 `*.svg`），或者更改为与主题捆绑的任何图标。
在 `mkdocs.yml` 中添加以下行：

=== ":octicons-image-16: Image"

    ``` yaml
    theme:
      logo: assets/logo.png
    ```

=== ":octicons-package-16: Icon, bundled"

    ``` yaml
    theme:
      icon:
        logo: material/library # (1)!
    ```

    1.  输入几个关键词，使用我们的[图标搜索]找到完美的图标，并点击短代码将其复制到您的剪贴板上：

        <div class="mdx-iconsearch" data-mdx-component="iconsearch">
          <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material library" />
          <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
            <div class="mdx-iconsearch-result__meta"></div>
            <ol class="mdx-iconsearch-result__list"></ol>
          </div>
        </div>

  [图标搜索]: ../reference/icons-emojis.md#search

通常，标题和侧边栏中的徽标链接到文档的首页，与 `site_url` 相同。可以通过以下配置更改此行为：

``` yaml
extra:
  homepage: https://example.com
```

### 网站图标 {#favicon}

<!-- md:version 0.1.0 -->
<!-- md:default [`assets/images/favicon.png`][Favicon default] -->

网站图标可以更改为指向位于 `docs` 文件夹中的用户提供的图片的路径。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  favicon: images/favicon.png
```

  [Favicon default]: https://github.com/squidfunk/mkdocs-material/blob/master/material/assets/images/favicon.png

### Site icons

[:octicons-tag-24: 9.2.0][Site icon support]

您在网站上看到的大多数图标，如导航图标，也可以更改。例如，要更改页脚中的导航箭头，请在 `mkdocs.yml` 中添加以下行：

```yaml
theme:
  icon:
    previous: fontawesome/solid/angle-left
    next: fontawesome/solid/angle-right
```

以下是主题使用的可自定义图标的完整列表：

| 图标名称    | 用途                                                                         |
|:-------------|:--------------------------------------------------------------------------|
| `logo`       | 参见 [徽标](#logo)                                                         |
| `menu`       | 打开抽屉                                                                   |
| `alternate`  | 更改语言                                                                   |
| `search`     | 搜索图标                                                                   |
| `share`      | 分享搜索                                                                   |
| `close`      | 重置搜索，关闭公告                                                          |
| `top`        | 返回顶部按钮                                                               |
| `edit`       | 编辑当前页面                                                               |
| `view`       | 查看页面源码                                                               |
| `repo`       | 仓库图标                                                                   |
| `admonition` | 参见 [警示图标](../reference/admonitions.md#admonition-icons)              |
| `tag`        | 参见 [标签图标和标识符](setting-up-tags.md#tag-icons-and-identifiers)        |
| `previous`   | 页脚中的上一页，移动设备上隐藏搜索                                             |
| `next`       | 页脚中的下一页

  [Site icon support]: https://github.com/squidfunk/mkdocs-material/releases/tag/9.2.0

## 自定义 {#customization}

### 额外图标 {#additional-icons}

为了使用自定义图标，[扩展主题]并在您想用于覆盖的[`custom_dir`][custom_dir]中创建一个名为 `.icons` 的新文件夹。接下来，将您的 `*.svg` 图标添加到 `.icons` 文件夹的子文件夹中。假设您下载并解压了 [Bootstrap] 图标集，并想将其添加到项目文档中。您的项目结构应该如下所示：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ .icons/
│     └─ bootstrap/
│        └─ *.svg
└─ mkdocs.yml
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
markdown_extensions:
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
      options:
        custom_icons:
          - overrides/.icons
```

您现在可以在 Markdown 文件中以及 `mkdocs.yml` 中的任何地方使用所有 :fontawesome-brands-bootstrap: Bootstrap 图标。
但是，请注意，语法略有不同：

- __在配置中使用图标__：从 `.icons` 文件夹开始取 `*.svg` 图标文件的路径并丢弃文件扩展名，例如，对于 `.icons/bootstrap/envelope-paper.svg`，使用：

    ``` yaml
    theme:
      icon:
        logo: bootstrap/envelope-paper
    ```

- __在 Markdown 文件中使用图标__：除了以上提到的从 `.icons` 文件夹取路径外，将所有 `/` 替换为 `-` 并用两个冒号包围图标短代码：

    ```
    :bootstrap-envelope-paper:
    ```

有关图标使用的进一步说明，请参阅 [图标参考]。

  [扩展主题]: ../customization.md#extending-the-theme
  [custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [Bootstrap]: https://icons.getbootstrap.com/
  [图标参考]: ../reference/icons-emojis.md#using-icons
