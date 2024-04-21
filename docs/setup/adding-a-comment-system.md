# 添加评论系统 {#adding-a-comment-system}

Material for MkDocs 允许通过使用[主题扩展]在任何页面的页脚轻松添加第三方评论系统。作为示例，我们将集成 [Giscus]，它是开源的、免费的，并使用 GitHub 讨论作为后端。

  [Giscus]: https://giscus.app/

## 自定义 {#customization}

### Giscus 集成 {#giscus-integration}

在您可以使用 [Giscus] 之前，需要完成以下步骤：

1.  __安装 [Giscus GitHub 应用]__ 并授权访问应该托管评论为 GitHub 讨论的仓库。请注意，这可以是与您的文档不同的仓库。
2.  __访问 [Giscus] 并通过其配置工具生成代码片段__ 以加载评论系统。复制下一步中的代码片段。生成的代码片段应类似于此：

    ``` html
    <script
      src="https://giscus.app/client.js"
      data-repo="<username>/<repository>"
      data-repo-id="..."
      data-category="..."
      data-category-id="..."
      data-mapping="pathname"
      data-reactions-enabled="1"
      data-emit-metadata="1"
      data-theme="light"
      data-lang="en"
      crossorigin="anonymous"
      async
    >
    </script>
    ```

[`comments.html`][comments] 部分（默认为空）是添加由 [Giscus] 生成的代码片段的最佳位置。按照[主题扩展]和[覆盖 `comments.html` 部分][覆盖部分]的指南操作：

``` html hl_lines="3"
{% if page.meta.comments %}
  <h2 id="__comments">{{ lang.t("meta.comments") }}</h2>
  <!-- Insert generated snippet here -->

  <!-- Synchronize Giscus theme with palette -->
  <script>
    var giscus = document.querySelector("script[src*=giscus]")

    // Set palette on initial load
    var palette = __md_get("__palette")
    if (palette && typeof palette.color === "object") {
      var theme = palette.color.scheme === "slate"
        ? "transparent_dark"
        : "light"

      // Instruct Giscus to set theme
      giscus.setAttribute("data-theme", theme) // (1)!
    }

    // Register event handlers after documented loaded
    document.addEventListener("DOMContentLoaded", function() {
      var ref = document.querySelector("[data-md-component=palette]")
      ref.addEventListener("change", function() {
        var palette = __md_get("__palette")
        if (palette && typeof palette.color === "object") {
          var theme = palette.color.scheme === "slate"
            ? "transparent_dark"
            : "light"

          // Instruct Giscus to change theme
          var frame = document.querySelector(".giscus-frame")
          frame.contentWindow.postMessage(
            { giscus: { setConfig: { theme } } },
            "https://giscus.app"
          )
        }
      })
    })
  </script>
{% endif %}
```

1.  此代码块确保当调色板设置为 `slate` 时，[Giscus] 使用暗主题渲染。请注意，有多个暗主题可供选择，因此您可以根据喜好更改它。

将突出显示的行替换为您在上一步中使用 [Giscus] 配置工具生成的代码片段。如果您从上面复制了代码片段，可以通过将 `comments` 前置属性设置为 `true` 来启用页面上的评论：

``` yaml
---
comments: true
---

# Page title
...
```

如果您希望为整个文件夹启用评论，可以使用[内置元插件]。

  [Giscus GitHub 应用]: https://github.com/apps/giscus
  [主题扩展]: ../customization.md#extending-the-theme
  [comments]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/comments.html
  [覆盖部分]: ../customization.md#overriding-partials
  [内置元插件]: ../plugins/meta.md
