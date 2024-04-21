# 更改颜色 {#changing-the-colors}

作为任何合适的 Material Design 实现，Material for MkDocs 支持谷歌的原始[调色板]，可以通过 `mkdocs.yml` 轻松配置。此外，可以使用 [CSS 变量][自定义颜色] 通过几行 CSS 来定制颜色，以符合您品牌的标识。

  [调色板]: http://www.materialui.co/colors
  [自定义颜色]: #custom-colors

## 配置 {#configuration}

### 调色板 {#color-palette}

#### 颜色方案 {#color-scheme}

<!-- md:version 5.2.0 -->
<!-- md:default `default` -->

Material for MkDocs 支持两种颜色方案：一种是简称为 `default` 的 __light mode__ ，另一种是称为 `slate` 的 __dark mode__ 。颜色方案可以通过 `mkdocs.yml` 设置：

``` yaml
theme:
  palette:
    scheme: default
```

点击砖块更改颜色方案：

<div class="mdx-switch">
  <button data-md-color-scheme="default"><code>default</code></button>
  <button data-md-color-scheme="slate"><code>slate</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-scheme]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      document.body.setAttribute("data-md-color-switching", "")
      var attr = this.getAttribute("data-md-color-scheme")
      document.body.setAttribute("data-md-color-scheme", attr)
      var name = document.querySelector("#__code_0 code span.l")
      name.textContent = attr
      setTimeout(function() {
        document.body.removeAttribute("data-md-color-switching")
      })
    })
  })
</script>

#### 主要颜色 {#primary-color}

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

主要颜色用于头部、侧边栏、文本链接和其他几个组件。要更改主要颜色，请将 `mkdocs.yml` 中的以下值设置为有效的颜色名称：

``` yaml
theme:
  palette:
    primary: indigo
```

点击砖块更改主要颜色：

<div class="mdx-switch">
  <button data-md-color-primary="red"><code>red</code></button>
  <button data-md-color-primary="pink"><code>pink</code></button>
  <button data-md-color-primary="purple"><code>purple</code></button>
  <button data-md-color-primary="deep-purple"><code>deep purple</code></button>
  <button data-md-color-primary="indigo"><code>indigo</code></button>
  <button data-md-color-primary="blue"><code>blue</code></button>
  <button data-md-color-primary="light-blue"><code>light blue</code></button>
  <button data-md-color-primary="cyan"><code>cyan</code></button>
  <button data-md-color-primary="teal"><code>teal</code></button>
  <button data-md-color-primary="green"><code>green</code></button>
  <button data-md-color-primary="light-green"><code>light green</code></button>
  <button data-md-color-primary="lime"><code>lime</code></button>
  <button data-md-color-primary="yellow"><code>yellow</code></button>
  <button data-md-color-primary="amber"><code>amber</code></button>
  <button data-md-color-primary="orange"><code>orange</code></button>
  <button data-md-color-primary="deep-orange"><code>deep orange</code></button>
  <button data-md-color-primary="brown"><code>brown</code></button>
  <button data-md-color-primary="grey"><code>grey</code></button>
  <button data-md-color-primary="blue-grey"><code>blue grey</code></button>
  <button data-md-color-primary="black"><code>black</code></button>
  <button data-md-color-primary="white"><code>white</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-primary]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-color-primary")
      document.body.setAttribute("data-md-color-primary", attr)
      var name = document.querySelector("#__code_1 code span.l")
      name.textContent = attr.replace("-", " ")
    })
  })
</script>

参阅下面的指南，了解如何设置[自定义颜色]。

#### 强调颜色 {#accent-color}

<!-- md:version 0.2.0 -->
<!-- md:default `indigo` -->

强调颜色用于标记可以互动的元素，例如悬停的链接、按钮和滚动条。它可以通过选择一个有效的颜色名称在
 `mkdocs.yml` 中更改：

``` yaml
theme:
  palette:
    accent: indigo
```

点击砖块更改强调颜色：

<style>
  .md-typeset button[data-md-color-accent] > code {
    background-color: var(--md-code-bg-color);
    color: var(--md-accent-fg-color);
  }
</style>

<div class="mdx-switch">
  <button data-md-color-accent="red"><code>red</code></button>
  <button data-md-color-accent="pink"><code>pink</code></button>
  <button data-md-color-accent="purple"><code>purple</code></button>
  <button data-md-color-accent="deep-purple"><code>deep purple</code></button>
  <button data-md-color-accent="indigo"><code>indigo</code></button>
  <button data-md-color-accent="blue"><code>blue</code></button>
  <button data-md-color-accent="light-blue"><code>light blue</code></button>
  <button data-md-color-accent="cyan"><code>cyan</code></button>
  <button data-md-color-accent="teal"><code>teal</code></button>
  <button data-md-color-accent="green"><code>green</code></button>
  <button data-md-color-accent="light-green"><code>light green</code></button>
  <button data-md-color-accent="lime"><code>lime</code></button>
  <button data-md-color-accent="yellow"><code>yellow</code></button>
  <button data-md-color-accent="amber"><code>amber</code></button>
  <button data-md-color-accent="orange"><code>orange</code></button>
  <button data-md-color-accent="deep-orange"><code>deep orange</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-accent]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-color-accent")
      document.body.setAttribute("data-md-color-accent", attr)
      var name = document.querySelector("#__code_2 code span.l")
      name.textContent = attr.replace("-", " ")
    })
  })
</script>

参阅下面的指南，了解如何设置[自定义颜色]。

### 切换调色板 {#color-palette-toggle}

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-toggle -->

提供浅色 _和_ 深色颜色调板使您的文档在一天中的不同时间易于阅读，因此用户可以相应选择。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  palette: # (1)!

    # Palette toggle for light mode
    - scheme: default
      toggle:
        icon: material/brightness-7 # (2)!
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

1.  注意现在将 `theme.palette` 设置定义为列表。

2.  输入一些关键词以使用我们的[图标搜索]找到完美的图标，并点击短代码将其复制到您的剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="brightness" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

此配置将在搜索栏旁边渲染一个颜色调板切换。注意，您还可以为每个颜色调板定义单独的[`primary`][palette.primary]和[`accent`][palette.accent]设置。

以下属性必须为每个切换设置：

<!-- md:option palette.toggle.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须指向一个有效的图标路径，引用主题中捆绑的任何图标，否则构建将不会成功。一些流行的组合包括：

    * :material-brightness-7: + :material-brightness-4: – `material/brightness-7` + `material/brightness-4`
    * :material-toggle-switch: + :material-toggle-switch-off-outline: – `material/toggle-switch` + `material/toggle-switch-off-outline`
    * :material-weather-night: + :material-weather-sunny: – `material/weather-night` + `material/weather-sunny`
    * :material-eye: + :material-eye-outline: – `material/eye` + `material/eye-outline`
    * :material-lightbulb: + :material-lightbulb-outline: – `material/lightbulb` + `material/lightbulb-outline`

<!-- md:option palette.toggle.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性用作切换的 `title` 属性，并应设置为一个可辨认的名称以提高可访问性。它被渲染为一个[tooltip]。

  [palette.scheme]: #color-scheme
  [palette.primary]: #primary-color
  [palette.accent]: #accent-color
  [图标搜索]: ../reference/icons-emojis.md#search
  [tooltip]: ../reference/tooltips.md

### 系统偏好 {#system-preference}

<!-- md:version 7.1.0 -->
<!-- md:default none -->
<!-- md:example color-palette-system-preference -->

每个颜色调板可以通过使用媒体查询链接到用户对浅色和深色外观的系统偏好。只需在 `mkdocs.yml` 中的 `scheme` 定义旁边添加一个 `media` 属性：

``` yaml
theme:
  palette:

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

当用户首次访问您的网站时，媒体查询按其定义的顺序进行评估。匹配的第一个媒体查询选择默认颜色调板。

#### 自动浅色/深色模式 {#automatic-light-dark-mode}

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->
<!-- md:example color-palette-system-preference -->

较新的操作系统允许在白天和夜间自动切换浅色和深色外观。Material for MkDocs 添加了对自动
浅色/深色模式的支持，将颜色调板选择委托给用户的操作系统。在 `mkdocs.yml` 中添加以下行：

``` yaml
theme:
  palette:

    # Palette toggle for automatic mode
    - media: "(prefers-color-scheme)"
      toggle:
        icon: material/brightness-auto
        name: Switch to light mode

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default # (1)!
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to system preference
```

1.  您还可以为每个颜色调板定义单独的[`primary`][palette.primary]和[`accent`][palette.accent]设置，即浅色和深色模式的不同颜色。

Material for MkDocs 现在将在操作系统在浅色和深色外观之间切换时更改颜色调板，即使用户没有重新加载站点。

  [Insiders]: ../insiders/index.md

## 自定义 {#customization}

### 自定义颜色 {#custom-colors}

<!-- md:version 5.0.0 -->
<!-- md:example custom-colors -->

Material for MkDocs 使用 [CSS 变量] (自定义属性) 实现颜色。如果您想自定义颜色以超出调板（例如使用您的品牌特定颜色），您可以添加[附加样式表]并调整 CSS 变量的值。

首先，在 `mkdocs.yml` 中将 [`primary`][palette.primary] 或 [`accent`][palette.accent] 值设置为 `custom`，以向主题发出信号，表明您想定义自定义颜色，例如，当您想覆盖 `primary` 颜色时：

``` yaml
theme:
  palette:
    primary: custom
```

假设您是 :fontawesome-brands-youtube:{ style="color: #EE0F0F" } __YouTube__，并希望将主要颜色设置为您品牌的调板。只需添加：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    :root {
      --md-primary-fg-color:        #EE0F0F;
      --md-primary-fg-color--light: #ECB7B7;
      --md-primary-fg-color--dark:  #90030C;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

参见包含[颜色定义]的文件，了解所有 CSS 变量的列表。

  [CSS 变量]: https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties
  [颜色定义]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/assets/stylesheets/main/_colors.scss
  [附加样式表]: ../customization.md#additional-css


### 自定义颜色方案 {#custom-color-schemes}

除了覆盖特定颜色外，您还可以通过将定义包装在 `[data-md-color-scheme="..."]`
[属性选择器] 中来创建自己的命名颜色方案，然后可以按照[颜色方案][palette.scheme]部分中描述的通过 `mkdocs.yml` 设置：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    [data-md-color-scheme="youtube"] {
      --md-primary-fg-color:        #EE0F0F;
      --md-primary-fg-color--light: #ECB7B7;
      --md-primary-fg-color--dark:  #90030C;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    theme:
      palette:
        scheme: youtube
    extra_css:
      - stylesheets/extra.css
    ```

此外，`slate` 颜色方案通过 `hsla` 颜色函数定义所有颜色，并从 `--md-hue` CSS 变量推导其颜
色。您可以调整 `slate` 主题：

``` css
[data-md-color-scheme="slate"] {
  --md-hue: 210; /* (1)! */
}
```

1.  `hue` 值必须在 `[0, 360]` 范围内

  [属性选择器]: https://www.w3.org/TR/selectors-4/#attribute-selectors
