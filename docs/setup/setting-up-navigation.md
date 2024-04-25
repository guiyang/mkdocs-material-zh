# 设置导航 {#setting-up-navigation}

清晰简洁的导航结构是良好项目文档的重要方面。Material for MkDocs 提供了多种选项来配置导航元素的行为，包括[标签页]和[段]，以及其一大特色功能：[即时加载]。

  [标签页]: #navigation-tabs
  [段]: #navigation-sections
  [即时加载]: #instant-loading

## 配置 {#configuration}

### 即时加载 {#instant-loading}

<!-- md:version 5.0.0 -->
<!-- md:feature -->

启用即时加载后，所有内部链接的点击都将通过 [XHR] 拦截并分派，无需完全重新加载页面。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.instant
```

结果页面将被解析和注入，所有事件处理程序和组件都将自动重新绑定，即 __Material for MkDocs 现在表现得像一个单页应用程序__。现在，搜索索引在导航中得以保留，这对于大型文档站点尤其有用。

!!! info "必须设置 [`site_url`][mkdocs.site_url]"

    注意，使用即时导航时必须设置 [`site_url`][mkdocs.site_url]，因为即时导航依赖于生成的 `sitemap.xml`，如果省略此设置，`sitemap.xml` 将为空。示例：

    ``` yaml
    site_url: https://example.com
    ```

  [XHR]: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

#### 即时预取 {#instant-prefetching}

<!-- md:sponsors -->
<!-- md:version insiders-4.36.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

即时预取是一个新的实验性功能，当用户将鼠标悬停在链接上时，它将开始获取页面。这将减少用户感知的加载时间，尤其是在慢速连接上，因为页面将在导航时立即可用。启用它：

``` yaml
theme:
  features:
    - navigation.instant
    - navigation.instant.prefetch
```

#### 进度指示器 {#progress-indicator}

<!-- md:version 9.4.3 -->
<!-- md:feature -->
<!-- md:flag experimental -->

为了在使用即时导航时在慢速连接上提供更好的用户体验，可以启用进度指示器。它将显示在页面顶部，并在页面完全加载后隐藏。您可以在 `mkdocs.yml` 中启用它：

``` yaml
theme:
  features:
    - navigation.instant
    - navigation.instant.progress
```

进度指示器只有在页面在 400 毫秒后仍未完成加载时才会显示，这样快速连接永远不会为了更好的即时体验而显示它。

### 即时预览 :material-alert-decagram:{ .mdx-pulse title="2024年1月28日添加" } {#instant-previews}

<!-- md:sponsors -->
<!-- md:version insiders-4.52.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

即时预览是一个全新的功能，允许用户预览您文档的另一个页面而不导航到该页面。它们可以非常有助于保持用户的上下文。即时预览可以在任何带有 `data-preview` 属性的标题链接上启用：

```` markdown title="带即时预览的链接"
``` markdown
[Attribute Lists](#){ data-preview }
```
````

<div class="result" markdown>

[属性列表](extensions/python-markdown.md#attribute-lists){ data-preview }

</div>

!!! info "限制"

    即时预览仍然是一个实验性功能，目前仅限于标题链接。这意味着，您可以在指向另一页上的标题的任何内部链接上使用它们，但不能用于其他带有 `id` 属性的元素。在我们收集到足够的反馈后，我们将考虑将此功能扩展到其他可能的任意元素。

#### 自动预览 {#automatic-previews}

<!-- md:sponsors -->
<!-- md:version insiders-4.53.0 -->
<!-- md:extension -->
<!-- md:flag experimental -->

与即时预览一起工作的推荐方法是使用 Material for MkDocs 包含的 Markdown 扩展，因为它允许您为文档的每个页面或每个部分启用即时预览：

``` yaml
markdown_extensions:
  - material.extensions.preview:
      targets:
        include:
          - changelog/index.md
          - customization.md
          - insiders/changelog/*
          - setup/extensions/*
```

以上配置是我们用于我们的文档的。我们为我们的更新日志、自定义指南和 Insiders 部分以及我们支持的所有 Markdown 扩展启用了即时预览。

!!! info "完整配置示例"

    ``` yaml
    markdown_extensions:
      - material.extensions.preview:
          sources: # (1)!
            include:
              - ...
            exclude:
              - ...
          targets: # (2)!
            include:
              - ...
            exclude:
              - ...
    ```

    1.  来源指定了应在其上启用即时预览的页面。如果省略此设置，将在所有页面上启用即时预览。您可以使用模式来包括或排除页面。排除是在包括之上评估的，所以如果一个页面同时被匹配，它将被排除。

    2.  目标指定了应启用即时预览的页面。这是启用即时预览的推荐方法。
---

即时预览也可以通过在 `mkdocs.yml` 中添加以下行来全局启用，这将启用所有标题链接的即时预览，从而无需添加数据属性：

``` yaml
theme:
  features:
    - navigation.instant.preview
```

!!! info "必须设置 [`site_url`][mkdocs.site_url]"

    注意，使用即时预览时必须设置 [`site_url`][mkdocs.site_url]，因为即时预览依赖于生成的 `sitemap.xml`，如果省略此设置，`sitemap.xml` 将为空。示例：

    ``` yaml
    site_url: https://example.com
    ```

### 锚点跟踪 {#anchor-tracking}

<!-- md:version 8.0.0 -->
<!-- md:feature -->

启用锚点跟踪时，地址栏中的 URL 将自动更新为在目录中高亮显示的活动锚点。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.tracking
```

### 导航标签 {#navigation-tabs}

<!-- md:version 1.1.0 -->
<!-- md:feature -->

启用标签后，顶级部分将在 `1220px` 以上的视口下呈现在标题下方的菜单层，但在移动设备上保持原样。[^1] 在 `mkdocs.yml` 中添加以下行：

  [^1]:
    在 <!-- md:version 6.2.0 --> 之前，导航标签的行为略有不同。在 `mkdocs.yml` 的 `nav` 条目中定义的所有顶级页面（即直接引用 `*.md` 文件的所有顶级条目）都被分组到第一个标签下，该标签采用第一页的标题。这使得无法将顶级页面（或外部链接）包含为标签项，如在 #1884 和 #2072 中报告的那样。从 <!-- md:version 6.2.0 --> 开始，导航标签包括所有顶级页面和段。

``` yaml
theme:
  features:
    - navigation.tabs
```

=== "启用标签"

    [![Navigation tabs enabled]][Navigation tabs enabled]

=== "未启用"

    [![Navigation tabs disabled]][Navigation tabs disabled]

  [Navigation tabs enabled]: ../assets/screenshots/navigation-tabs.png
  [Navigation tabs disabled]: ../assets/screenshots/navigation.png

#### 粘性导航标签 {#sticky-navigation-tabs}

<!-- md:version 7.3.0 -->
<!-- md:feature -->

启用粘性标签时，导航标签将锁定在页眉下方，并在向下滚动时始终可见。只需在 `mkdocs.yml` 中添加以下两个功能标志：

``` yaml
theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky
```

=== "启用粘性标签"

    [![Sticky navigation tabs enabled]][Sticky navigation tabs enabled]

=== "未启用"

    [![Sticky navigation tabs disabled]][Sticky navigation tabs disabled]

  [Sticky navigation tabs enabled]: ../assets/screenshots/navigation-tabs-sticky.png
  [Sticky navigation tabs disabled]: ../assets/screenshots/navigation-tabs-collapsed.png

### 导航分区 {#navigation-sections}

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用分区时，顶级分区将在 `1220px` 以上的视口中作为组在侧边栏中呈现，但在移动设备上保持原样。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.sections
```

=== "启用分区"

    [![Navigation sections enabled]][Navigation sections enabled]

=== "未启用"

    [![Navigation sections disabled]][Navigation sections disabled]

  [Navigation sections enabled]: ../assets/screenshots/navigation-sections.png
  [Navigation sections disabled]: ../assets/screenshots/navigation.png

两个功能标志，[`navigation.tabs`][标签页] 和 [`navigation.sections`][段]，可以相互组合。如果两个功能标志均已启用，则将为第二级导航项呈现分区。

### 导航展开 {#navigation-expansion}

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用展开时，左侧边栏将默认展开所有可折叠的子分区，用户无需手动打开子分区。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.expand
```

=== "启用展开"

    [![Navigation expansion enabled]][Navigation expansion enabled]

=== "未启用"

    [![Navigation expansion disabled]][Navigation expansion disabled]

  [Navigation expansion enabled]: ../assets/screenshots/navigation-expand.png
  [Navigation expansion disabled]: ../assets/screenshots/navigation.png

### 导航路径 <small>面包屑导航</small> {#navigation-path}

<!-- md:sponsors -->
<!-- md:version insiders-4.28.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用导航路径时，每个页面的标题上方将呈现面包屑导航，这可能会使访问您的文档的用户更易于定位。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.path
```

=== "启用导航路径"

    [![Navigation path enabled]][Navigation path enabled]

=== "未启用"

    [![Navigation path disabled]][Navigation path disabled]

  [Navigation path enabled]: ../assets/screenshots/navigation-path-on.png
  [Navigation path disabled]: ../assets/screenshots/navigation-path-off.png

### 导航修剪 {#navigation-pruning}

<!-- md:version 9.2.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用修剪时，只有可见的导航项会包含在渲染的HTML中，__减少构建站点的大小33%或更多__。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.prune # (1)!
```

1.  此功能标志与[`navigation.expand`][navigation.expand] 不兼容，因为导航展开需要完整的导航结构。

此功能标志特别适用于拥有100+甚至1000+页面的文档站点，因为导航占据了HTML的很大一部分。导航修剪将用链接替换所有可展开的分区，链接到该分区的第一个页面（或分区索引页面）。

  [navigation.expand]: #navigation-expansion

### 分区索引页面 {#section-index-pages}

<!-- md:version 7.3.0 -->
<!-- md:feature -->

启用分区索引页面时，文档可以直接附加到分区，这对于提供概览页面特别有用。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.indexes # (1)!
```

1.  此功能标志与 [`toc.integrate`][toc.integrate] 不兼容，因为由于空间不足，分区无法托管目录表。

=== "启用分区索引页面"

    [![Section index pages enabled]][Section index pages enabled]

=== "未启用"

    [![Section index pages disabled]][Section index pages disabled]

要将页面链接到某个分区，请在相应文件夹中创建一个名为 `index.md` 的新文档，并将其添加到您的导航分区的开头：

``` yaml
nav:
  - Section:
    - section/index.md # (1)!
    - Page 1: section/page-1.md
    ...
    - Page n: section/page-n.md
```

1.  MkDocs 也将名为 `README.md` 的文件视为 [index pages]。

  [Section index pages enabled]: ../assets/screenshots/navigation-index-on.png
  [Section index pages disabled]: ../assets/screenshots/navigation-index-off.png
  [toc.integrate]: #navigation-integration
  [index pages]: https://www.mkdocs.org/user-guide/writing-your-docs/#index-pages

### 目录表 {#table-of-contents}

#### 锚点跟随 {#anchor-following}

<!-- md:version 8.5.0 -->
<!-- md:feature -->
<!-- md:flag experimental -->

启用[目录表]的锚点跟随后，边栏会自动滚动，以便活动锚点始终可见。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - toc.follow
```

#### 导航集成 {#navigation-integration}

<!-- md:version 6.2.0 -->
<!-- md:feature -->

启用[目录表]的导航集成后，它将始终作为左侧导航边栏的一部分进行呈现。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - toc.integrate # (1)!
```

1.  此功能标志与 [`navigation.indexes`][navigation.indexes] 不兼容，因为由于空间不足，分区无法托管目录表。

=== "启用导航集成"

    [![Navigation integration enabled]][Navigation integration enabled]

=== "未启用"

    [![Navigation integration disabled]][Navigation integration disabled]

  [目录表]: extensions/python-markdown.md#table-of-contents
  [Navigation integration enabled]: ../assets/screenshots/toc-integrate.png
  [Navigation integration disabled]: ../assets/screenshots/navigation-tabs.png
  [navigation.indexes]: #section-index-pages

### 回到顶部按钮 {#back-to-top-button}

<!-- md:version 7.1.0 -->
<!-- md:feature -->

当用户向下滚动后开始向上滚动时，可以显示回到顶部按钮。它位于页眉下方居中呈现。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  features:
    - navigation.top
```

## 使用方法 {#usage}

### 隐藏侧边栏 {#hiding-the-sidebars}

<!-- md:version 6.2.0 -->
<!-- md:flag metadata -->

可以通过前置属性 `hide` 隐藏文档的导航和/或目录表侧边栏。在 Markdown 文件顶部添加以下行：

``` yaml
---
hide:
  - navigation
  - toc
---

# Page title
...
```

=== "隐藏导航"

    [![Hide navigation enabled]][Hide navigation enabled]

=== "隐藏目录表"

    [![Hide table of contents enabled]][Hide table of contents enabled]

=== "隐藏两者"

    [![Hide both enabled]][Hide both enabled]

  [Hide navigation enabled]: ../assets/screenshots/hide-navigation.png
  [Hide table of contents enabled]: ../assets/screenshots/hide-toc.png
  [Hide both enabled]: ../assets/screenshots/hide-navigation-toc.png

### 隐藏导航路径 {#hiding-the-navigation-path}

<!-- md:sponsors -->
<!-- md:version insiders-4.28.0 -->
<!-- md:flag metadata -->

虽然[导航路径]显示在主标题上方，有时可能需要针对特定页面隐藏它，可以通过前置属性 `hide` 来实现：

``` yaml
---
hide:
  - path
---

# Page title
...
```

  [导航路径]: #navigation-path

## 自定义 {#customization}

### 键盘快捷键 {#keyboard-shortcuts}

Material for MkDocs 包括多个键盘快捷键，使您能够通过键盘导航项目文档。有两种模式：

<!-- md:option mode:search -->

:   当 _搜索被聚焦_ 时，此模式激活。它提供多个键绑定以通过键盘访问和导航搜索：

    * ++arrow-down++ , ++arrow-up++ : select next / previous result
    * ++esc++ , ++tab++ : close search dialog
    * ++enter++ : follow selected result

<!-- md:option mode:global -->

:   当 _搜索未被聚焦_ 且没有其他可能接受键盘输入的元素被聚焦时，此模式激活。以下键被绑定：

    * ++f++ , ++s++ , ++slash++ : open search dialog
    * ++p++ , ++comma++ : go to previous page
    * ++n++ , ++period++ : go to next page

假设您想将某个操作绑定到 ++x++ 键。通过使用[附加JavaScript]，您可以订阅 `keyboard$` 可观察对象并附加自定义事件监听器：

=== ":octicons-file-code-16: `docs/javascripts/shortcuts.js`"

    ``` js
    keyboard$.subscribe(function(key) {
      if (key.mode === "global" && key.type === "x") {
        /* Add custom keyboard handler here */
        key.claim() // (1)!
      }
    })
    ```

    1.  调用 `key.claim()` 将在底层事件上执行 `preventDefault()`，因此按键不会进一步传播并影响其他事件监听器。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/shortcuts.js
    ```

  [附加JavaScript]: ../customization.md#additional-javascript

### 内容区域宽度 {#content-area-width}

内容区域的宽度设置为每行的长度不超过80-100个字符，具体取决于字符的宽度。虽然这是一个合理的默认值，因为较长的行往往更难阅读，但可能希望增加内容区域的整体宽度，甚至使其扩展到可用空间的整个区域。

这可以通过一个[附加样式表]和几行CSS轻松实现：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .md-grid {
      max-width: 1440px; /* (1)! */
    }
    ```

    1.  如果您希望内容区域始终扩展到可用的屏幕空间，请使用以下CSS重置 `max-width`：

        ``` css
        .md-grid {
          max-width: initial;
        }
        ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

  [additional style sheet]: ../customization.md#additional-css
