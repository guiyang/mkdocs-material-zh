# 设置社交卡片 {#setting-up-social-cards}

Material for MkDocs 可以为您的文档自动创建精美的社交卡片，这些卡片将作为社交媒体平台上的链接预览显示。您可以从几个[预设计的布局][默认布局]中选择，或创建[自定义布局]以匹配您独特的风格和品牌形象。

---

:fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__[如何构建自定义社交卡片]__ 作者 @james-willett – :octicons-clock-24: 24分钟 – 学习如何自动为每个页面完美匹配您的品牌创建完全自定义的社交卡片！

  [如何构建自定义社交卡片]: https://www.youtube.com/watch?v=4OjnOc6ftJ8

<figure markdown>

[![Layout default variant]][Layout default variant]

  <figcaption markdown>

我们[格式化]参考的社交卡片

  </figcaption>
</figure>

  [默认布局]: ../plugins/social.md#layouts
  [自定义布局]: #customization
  [格式化]: ../reference/formatting.md
  [Layout default variant]: ../assets/screenshots/social-cards-variant.png

## 配置 {#configuration}

### 内置社交插件 {#built-in-social-plugin}

<!-- md:version 8.5.0 -->
<!-- md:plugin -->
<!-- md:flag experimental -->

内置社交插件自动为每个页面生成自定义预览图像。安装所有[图像处理依赖项]并在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - social
```

有关所有设置的列表，请参阅 [插件文档]。

  [插件文档]: ../plugins/social.md

!!! info "必须设置 [`site_url`][site_url]"

    请注意，使用社交插件时必须设置 [`site_url`][site_url]，否则生成的卡片将无法正确链接。社交媒体服务如 Twitter 和 Facebook 要求社交预览指向绝对 URL，插件只有在设置了 [`site_url`][site_url] 时才能计算出来。示例：

    ``` yaml
    site_url: https://example.com
    ```

  [图像处理依赖项]: ../plugins/requirements/image-processing.md
  [site_url]: https://www.mkdocs.org/user-guide/configuration/#site_url

## 使用 {#usage}

如果您想调整社交卡片的标题或设置自定义描述，您可以设置前 matter [`title`][更改标题] 和 [`description`][更改描述] 属性，这些属性优先于默认值，或使用：

- [`cards_layout_options.title`](../plugins/social.md#option.title)
- [`cards_layout_options.description`](../plugins/social.md#option.description)

  [更改标题]: ../reference/index.md#setting-the-page-title
  [更改描述]: ../reference/index.md#setting-the-page-description

### 选择字体 {#choosing-a-font}

某些字体不包含 CJK 字符，例如 [默认字体，`Roboto`][font]。如果您的 `site_name`、`site_description` 或页面标题包含 CJK 字符，请从 [Google Fonts] 中选择带有 CJK 字符的其他字体，例如 `Noto Sans` 字体系列：

=== "简体中文"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans SC
    ```

=== "繁体中文"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans TC
    ```

=== "日本语"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans JP
    ```

=== "韩语"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            font_family: Noto Sans KR
    ```

  [font]: changing-the-fonts.md#regular-font

### 更改布局 {#changing-the-layout}

<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:flag experimental -->

如果您想为单个页面使用不同的布局（例如您的着陆页），您可以使用 `social` 前 matter 属性与 [`cards_layout`](../plugins/social.md#meta.social.cards_layout) 键，就像在 `mkdocs.yml` 中一样：

``` yaml
---
social:
  cards_layout: custom
---

# Page title
...
```

您可以为文档的整个子树应用这些更改，例如，通过使用 [内置元数据插件] 为您的博客和 API 参考生成不同的社交卡片。

  [内置元数据插件]: ../plugins/meta.md

### 参数化布局 {#parametrizing-the-layout}

<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:flag experimental -->

除了更改整个布局外，您还可以覆盖布局公开的所有选项。这意味着您可以使用自定义前 matter 属性参数化社交卡片，例如 `tags`、`date`、`author` 或您能想到的任何内容。只需定义 [`cards_layout_options`](../plugins/social.md#meta.social.cards_layout_options)：

``` yaml
---
social:
  cards_layout_options:
    background_color: blue # Change background color
    background_image: null # Remove background image
---

# Page title
...
```

您可以为文档的整个子树应用这些更改，例如，通过使用 [内置元数据插件] 为您的博客和 API 参考生成不同的社交卡片。

### 禁用社交卡片 {#disabling-social-cards}

<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:flag experimental -->

如果您希望禁用某个页面的社交卡片，只需在 Markdown 文档的前 matter 中添加以下内容：

``` yaml
---
social:
  cards: false
---

# Page title
...
```

## 自定义 {#customization}

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:flag experimental -->

[Insiders] 发布了 [内置社交插件] 的全新重写版本，并引入了基于 YAML 和 [Jinja 模板] 的全新布局系统——同样的引擎 Material for MkDocs 用于 HTML 模板——允许创建复杂的自定义布局：

<div class="mdx-social">
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 0</span>
      <img src="../../assets/screenshots/social-cards-layer-0.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 1</span>
      <img src="../../assets/screenshots/social-cards-layer-1.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 2</span>
      <img src="../../assets/screenshots/social-cards-layer-2.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 3</span>
      <img src="../../assets/screenshots/social-cards-layer-3.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 4</span>
      <img src="../../assets/screenshots/social-cards-layer-4.png" />
    </div>
  </div>
  <div class="mdx-social__layer">
    <div class="mdx-social__image">
      <span class="mdx-social__label">Layer 5</span>
      <img src="../../assets/screenshots/social-cards-layer-5.png" />
    </div>
  </div>
</div>

社交卡片由层组成，类似于它们在 Adobe Photoshop 等图形设计软件中的表示。由于许多层在为每个页面生成的卡片中都很常见（例如，背景或徽标），内置社交插件可以自动去重层并只渲染一次，大大加快了卡片生成的速度。生成的卡片被缓存以确保仅在其内容更改时重新生成。

布局以 YAML 语法编写。在开始创建自定义布局之前，最好[研究预设计的布局]（链接到 [Insiders] 仓库），以更好地了解它们的工作方式。然后，创建一个新的布局并在 `mkdocs.yml` 中引用它：

=== ":octicons-file-code-16: `layouts/custom.yml`"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers: []
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    plugins:
      - social:
          cards_layout_dir: layouts
          cards_layout: custom
          debug: true
    ```

请注意，应省略 `.yml` 文件扩展名。接下来，运行 `mkdocs serve`，并查看 `.cache` 目录中生成的卡片。在编辑器中打开任何卡片，以便您可以立即看到更改。由于我们没有定义任何层，卡片是透明的。

以下部分解释如何创建自定义布局。

  [Insiders]: ../insiders/index.md
  [内置社交插件]: ../plugins/social.md
  [Google Fonts]: https://fonts.google.com/
  [Jinja 模板]: https://jinja.palletsprojects.com/en/3.1.x/
  [研究预设计的布局]: https://github.com/squidfunk/mkdocs-material-insiders/tree/master/src/plugins/social/layouts

### 尺寸和偏移 {#size-and-offset}

每个层都有相关的尺寸和偏移，这些都是以像素定义的。`size` 通过 `width` 和 `height` 属性定义，而 `offset` 通过 `x` 和 `y` 属性定义：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - size: { width: 1200, height: 630 }
    offset: { x: 0, y: 0 }
```

如果省略了 `size`，它默认为布局的大小。如果省略了 `offset`，它默认为左上角，这是默认的 `origin`。保存布局并重新加载渲染：

![Layer size]

因为我们在 `mkdocs.yml` 中启用了 [`debug`][debug] 模式，所以可以看到图层轮廓和网格。左上角显示了图层索引和偏移，这对于对齐和组合很有用。

  [Layer size]: ../assets/screenshots/social-cards-layer-size.png
  [debug]: ../plugins/social.md#debugging

#### 原点 {#origin}

<!-- md:version insiders-4.35.0 -->
<!-- md:flag experimental -->

`x` 和 `y` 值的 `origin` 可以更改，以便图层与布局的某个边缘或角落对齐，例如，与布局的右下角对齐：

``` yaml hl_lines="5"
size: { width: 1200, height: 630 }
layers:
  - size: { width: 1200, height: 630 }
    offset: { x: 0, y: 0 }
    origin: end bottom
```

下表显示了支持的值：

<figure markdown>

| Origin         |                 |              |
| -------------- | --------------- | ------------ |
| :material-arrow-top-left:    `start top`    | :material-arrow-up:     `center top`    | :material-arrow-top-right:    `end top`    |
| :material-arrow-left:        `start center` | :material-circle-small: `center`        | :material-arrow-right:        `end center` |
| :material-arrow-bottom-left: `start bottom` | :material-arrow-down:   `center bottom` | :material-arrow-bottom-right: `end bottom` |

  <figcaption>
    支持的原点值
  </figcaption>
</figure>

### 背景 {#backgrounds}

每个图层可以分配背景颜色和图像。如果同时给定了颜色和图像，则颜色将渲染在图像上方，允许半透明、着色背景：

=== "背景颜色"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          color: "#4051b5"
    ```

    ![Layer background color]

=== "背景图像"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          image: layouts/background.png
    ```

    ![Layer background image]

=== "背景图像，着色"

    ``` yaml
    size: { width: 1200, height: 630 }
    layers:
      - background:
          image: layouts/background.png
          color: "#4051b5ee" # (1)!
    ```

    1.  颜色值可以设置为 [CSS color keyword]，或者是 3、4、6 或 8 位的 HEX 颜色代码，允许半透明图层。

    ![Layer background]

背景图像会自动缩放以适应图层，同时保持纵横比。注意我们省略了 `size` 和 `offset`，因为我们希望填充整个社交卡片的区域。

[Layer background color]: ../assets/screenshots/social-cards-layer-background-color.png
[Layer background image]: ../assets/screenshots/social-cards-layer-background-image.png
[Layer background]: ../assets/screenshots/social-cards-layer-background.png

### 排版 {#typography}

现在，我们可以添加从 Markdown 文件中获取的动态排版——这是 [内置社交插件] 的真正存在的理由。 [Jinja 模板] 用于渲染然后添加到图像上的文本字符串：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - size: { width: 832, height: 310 }
    offset: { x: 62, y: 160 }
    typography:
      content: "{{ page.title }}" # (1)!
      align: start
      color: white
      line:
        amount: 3
        height: 1.25
      font:
        family: Roboto
        style: Bold
```

1.  在 [Jinja 模板] 中可以使用以下变量：

    - [`config.*`][config variable]
    - [`page.*`][page variable]
    - [`layout.*`][layout options]

    作者可以自由定义 `layout.*` 选项，这些选项可用于从 `mkdocs.yml` 向布局传递任意数据。

这将呈现一个带有页面标题的文本层，行高为1.25，最多3行。插件会根据行高、行数和字体度量（如升高和降低）自动计算字体大小。[^2] 这将呈现：

  [^2]:
    如果插件要求作者手动指定字体大小和行高，就无法保证文本能够适应图层。因此，我们采用了声明式方法，作者指定所需的行高和行数，插件自动计算字体大小。

![Layer typography]

  [config variable]: https://www.mkdocs.org/dev-guide/themes/#config
  [page variable]: https://www.mkdocs.org/dev-guide/themes/#page
  [Layer typography]: ../assets/screenshots/social-cards-layer-typography.png

#### 溢出 {#overflow}

如果文本溢出图层，有两种可能的行为：文本自动截断并以省略号缩短，或者文本自动缩小以适应图层：

``` { .markdown .no-copy }
# If we use a very long headline, we can see how the text will be truncated
```

=== ":octicons-ellipsis-16: Ellipsis"

    ![Layer typography ellipsis]

=== ":material-arrow-collapse: Shrink"

    ![Layer typography shrink]

虽然默认是截断并使用省略号，但可以通过将 `overflow` 设置为 `shrink` 来启用自动缩小：

``` yaml hl_lines="7"
size: { width: 1200, height: 630 }
layers:
  - size: { width: 832, height: 310 }
    offset: { x: 62, y: 160 }
    typography:
      content: "{{ page.title }}"
      overflow: shrink
      align: start
      color: white
      line:
        amount: 3
        height: 1.25
      font:
        family: Roboto
        style: Bold
```

  [Layer typography ellipsis]: ../assets/screenshots/social-cards-layer-typography-ellipsis.png
  [Layer typography shrink]: ../assets/screenshots/social-cards-layer-typography-shrink.png

#### 对齐 {#alignment}

文本可以对齐到图层的所有角落和边缘。例如，如果我们想要将文本对齐到图层的中间，我们可以将 `align` 设置为 `start center`，将呈现为：

![Layer typography align]

  [Layer typography align]: ../assets/screenshots/social-cards-layer-typography-align.png

下表显示了支持的值：

<figure markdown>

| Alignment      |                 |              |
| -------------- | --------------- | ------------ |
| :material-arrow-top-left:    `start top`    | :material-arrow-up:     `center top`    | :material-arrow-top-right:    `end top`    |
| :material-arrow-left:        `start center` | :material-circle-small: `center`        | :material-arrow-right:        `end center` |
| :material-arrow-bottom-left: `start bottom` | :material-arrow-down:   `center bottom` | :material-arrow-bottom-right: `end bottom` |

  <figcaption>
    Supported values for text alignment
  </figcaption>
</figure>

#### 字体 {#font}

[内置社交插件] 与 [Google Fonts] 集成，并将自动下载字体文件。`font` 属性接受一个 `family` 和 `style` 属性，其中 `family` 必须设置为字体名称，`style` 设置为支持的字体样式之一。例如，将 `family` 设置为 `Roboto` 将自动下载以下文件：

``` { .sh .no-copy #example }
.cache/plugins/social/fonts
└─ Roboto/
    ├─ Black.ttf
    ├─ Black Italic.ttf
    ├─ Bold.ttf
    ├─ Bold Italic.ttf
    ├─ Italic.ttf
    ├─ Light.ttf
    ├─ Light Italic.ttf
    ├─ Medium.ttf
    ├─ Medium Italic.ttf
    ├─ Regular.ttf
    ├─ Thin.ttf
    └─ Thin Italic.ttf
```

在这种情况下，作者可以使用 `Bold` 或 `Medium Italic` 作为 `style`。如果图层中指定的字体样式不属于字体家族的一部分，字体总是回退到 `Regular` 并在 [`debug`][debug] 模式下打印警告，因为所有字体家族都包括 `Regular`。

### 图标 {#icons}

作者可以利用 Material for MkDocs 提供的全部图标范围，甚至可以通过使用主题扩展并按照 [additional icons] 中描述的过程提供自定义图标。图标甚至可以通过使用 `color` 属性进行着色：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - background:
      color: "#4051b5"
  - size: { width: 144, height: 144 }
    offset: { x: 992, y: 64 }
    icon:
      value: material/cat
      color: white
```

这将在社交卡片的右上角呈现图标：

![Layer icon]

例如，图标可以用来绘制形状，如圆圈：

``` yaml
size: { width: 1200, height: 630 }
layers:
  - background:
      color: "#4051b5"
  - size: { width: 2400, height: 2400 }
    offset: { x: -1024, y: 64 }
    icon:
      value: material/circle
      color: "#5c6bc0"
  - size: { width: 1800, height: 1800 }
    offset: { x: 512, y: -1024 }
    icon:
      value: material/circle
      color: "#3949ab"
```

这将在背景中添加两个圆圈：

![Layer icon circles]

### 标签 {#tags}

新的 [内置社交插件] 提供了完全的灵活性，用于添加到您的网站的元标签，这些标签是向 Twitter 或 Discord 等服务说明如何显示您的社交卡片所必需的。所有默认布局都使用以下一组标签，您可以将其复制到您的布局中并进行调整：

``` yaml
definitions:

  - &page_title_with_site_name >-
    {%- if not page.is_homepage -%}
      {{ page.meta.get("title", page.title) }} - {{ config.site_name }}
    {%- else -%}
      {{ page.meta.get("title", page.title) }}
    {%- endif -%}

  - &page_description >-
    {{ page.meta.get("description", config.site_description) or "" }}

tags:

  og:type: website
  og:title: *page_title_with_site_name
  og:description: *page_description
  og:image: "{{ image.url }}"
  og:image:type: "{{ image.type }}"
  og:image:width: "{{ image.width }}"
  og:image:height: "{{ image.height }}"
  og:url: "{{ page.canonical_url }}"

  twitter:card: summary_large_image
  twitter:title: *page_title_with_site_name
  twitter:description: *page_description
  twitter:image: "{{ image.url }}"
```

请注意，此示例使用 [YAML anchors] 来减少重复。`definitions` 属性仅用于定义别名，然后可以使用锚点引用。

  [YAML anchors]: https://support.atlassian.com/bitbucket-cloud/docs/yaml-anchors/

__您是否觉得缺少了什么？请[开启讨论]告诉我们！__

  [additional icons]: ./changing-the-logo-and-icons.md#additional-icons
  [Layer icon]: ../assets/screenshots/social-cards-layer-icon.png
  [Layer icon circles]: ../assets/screenshots/social-cards-layer-icon-circles.png
  [开启讨论]: https://github.com/squidfunk/mkdocs-material/discussions/new
