---
title: 内置社交插件
icon: material/share-circle
---

# 内置社交插件 {#built-in-social-plugin}

社交插件自动智能地为您项目的每个页面生成美观且高度可定制的社交卡片，这些社交卡片在不同的[布局][default layouts]中呈现，当您或其他人在社交媒体上分享项目链接时显示为预览图像。

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件会为项目的每个页面自动生成可定制的社交卡片，当在社交媒体上分享项目链接时，这些卡片将作为预览图像出现，无需使用外部服务，只需[一行配置][configuration]。

通过使用高效的[图像处理]库，插件允许定义社交卡片的[自定义布局]，这些布局可以适应您的项目风格和品牌定位。尽管技术上使用像[Puppeteer][^1]这样的Web浏览器和自动化框架来生成社交卡片要简单得多，但这将为您的工具链增加额外的负担，可能使构建管道变得更加复杂、资源消耗更大，并显著降低速度。

  [^1]:
    [GitHub在其博客中写到]，他们使用[Puppeteer]为仓库、问题、提交、讨论以及在社交媒体上分享时出现的几乎所有其他内容生成社交卡片图像。

生成的社交卡片被[缓存]并存储在[`site`目录][mkdocs.site_dir]中，因此是自托管的，确保您的项目不依赖外部服务。为了生成社交卡片图像，您的系统上需要安装一些[依赖项]。

  [configuration]: #configuration
  [图像处理]: requirements/image-processing.md
  [自定义布局]: ../setup/setting-up-social-cards.md#customization
  [Puppeteer]: https://github.com/puppeteer/puppeteer
  [GitHub在其博客中写到]: https://github.blog/2021-06-22-framework-building-open-graph-images/
  [缓存]: #caching
  [依赖项]: #configuration

### 何时使用它 {#when-to-use-it}

有一种情况我们不推荐使用该插件：当您构建[离线可用文档]以提供下载时。否则，启用插件总是有意义的，因为在社交媒体上分享的您的文档链接会显得更具吸引力。

更有趣的是，该插件可以与 Material for MkDocs 提供的其他内置插件结合使用，以创建针对您的项目的复杂构建管道：

<div class="grid cards" markdown>

-   :material-newspaper-variant-outline: &nbsp; __[内置博客插件][blog]__

    ---

    社交插件自动为每篇文章和页面生成美观且可定制的社交卡片，显示在社交媒体上的预览中。

    ---

    __在社交媒体上分享的博客链接将呈现美观的社交卡片__

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件可以用来[更改][meta.social.cards_layout]社交卡片的布局或[更改特定布局选项][meta.social.cards_layout_options]，如[背景][option.background_color]或[颜色][option.color]，用于部分页面。

    ---

    __您的文档可以为每个部分使用完全不同的社交卡片__

</div>

  [离线可用文档]: ../setup/building-for-offline-usage.md
  [blog]: blog.md
  [meta]: meta.md

## 配置 {#configuration}

<!-- md:version 8.5.0 -->
<!-- md:plugin [social] – built-in -->
<!-- md:flag multiple -->
<!-- md:flag experimental -->

要开始使用社交插件，只需将以下行添加到`mkdocs.yml`，观察 Material for MkDocs 如何为您生成美观的社交卡片：

``` yaml
plugins:
  - social
```

社交插件已内置于 Material for MkDocs 中，无需安装。

但是，为了生成社交卡片图像，如果系统上尚未安装，需要安装[图像处理]的依赖项。链接的指南包括几个操作系统的说明，并提及一些替代环境。

  [social]: social.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 8.5.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。如果您想禁用插件，例如，对于本地构建，您可以在`mkdocs.yml`中使用[环境变量][mkdocs.env]：

``` yaml
plugins:
  - social:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

  [构建您的项目]: ../creating-your-site.md#building-your-site

---

#### <!-- md:setting config.concurrency -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default available CPUs - 1 -->

有更多的CPU可用时，插件可以并行处理更多工作，从而更快地完成社交卡片的生成。如果您想完全禁用并行处理，请使用：

``` yaml
plugins:
  - social:
      concurrency: 1
```

默认情况下，插件使用所有可用的CPU - 1，最少为1。

### 缓存 {#caching}

插件实现了一个[智能缓存]机制，确保只有在内容更改或未包含在缓存中时才重新生成社交卡片。如果布局中使用的任何变量发生变化，插件会检测到并重新生成社交卡片。

以下设置适用于缓存：

  [智能缓存]: requirements/caching.md

---

#### <!-- md:setting config.cache -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `true` -->

使用此设置指示插件绕过缓存，以便为所有页面重新生成社交卡片，即使缓存可能并未过期。通常不需要指定此设置，除非在调试插件本身时。可以使用以下方法禁用缓存：

``` yaml
plugins:
  - social:
      cache: false
```

---

#### <!-- md:setting config.cache_dir -->

<!-- md:version 8.5.0 -->
<!-- md:default `.cache/plugin/social` -->

通常不需要指定此设置，除非您想更改根目录内社交卡片图像缓存的路径。如果您想更改它，请使用：

``` yaml
plugins:
  - social:
      cache_dir: my/custom/dir
```

如果您正在使用[多个实例]的插件，为每个实例设置不同的缓存目录可能是个好主意，这样它们就不会相互干扰。

  [多个实例]: index.md#multiple-instances

### 日志记录 {#logging}

以下设置可用于日志记录：

---

#### <!-- md:setting config.log -->

<!-- md:sponsors -->
<!-- md:version insiders-4.40.2 -->
<!-- md:default `true` -->

使用此设置控制插件在生成社交卡片时是否仅记录错误而不终止构建，例如，图标的无效引用。要终止构建，请使用：

``` yaml
plugins:
  - social:
      log: false
```

---

#### <!-- md:setting config.log_level -->

<!-- md:sponsors -->
<!-- md:version insiders-4.40.2 -->
<!-- md:default `warn` -->

使用此设置控制插件在遇到错误时应使用的日志级别，这要求启用[`log`][config.log]设置。以下日志级别可用：

=== "`warn`"

    ``` yaml
    plugins:
      - social:
          log_level: warn
    ```

    错误作为警告报告，终止构建在[`strict`][mkdocs.strict] 模式下。

=== "`info`"

    ``` yaml
    plugins:
      - social:
          log_level: info
    ```

    错误仅作为信息性消息报告。

=== "`ignore`"

    ``` yaml
    plugins:
      - social:
          log_level: ignore
    ```

    错误仅在使用`--verbose`标志时报告。

### 社交卡片 {#social-cards}

以下设置可用于社交卡片生成：

---

#### <!-- md:setting config.cards -->

<!-- md:version 8.5.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用社交卡片生成。目前，插件的唯一目的是生成社交卡片，因此等同于[`enabled`][config.enabled]设置，但未来可能会添加其他功能。如果您想禁用社交卡片生成，请使用：

``` yaml
plugins:
  - social:
      cards: false
```

---

#### <!-- md:setting config.cards_dir -->

<!-- md:version 8.5.0 -->
<!-- md:default `assets/images/social` -->

通常不需要指定此设置，除非您想更改[`site`目录][mkdocs.site_dir]内存储社交卡片的路径。如果您想更改它，请使用：

``` yaml
plugins:
  - social:
      cards_dir: my/custom/dir
```

此配置将生成的图像存储在[`site`目录][mkdocs.site_dir]的`my/custom/dir`中。

---

#### <!-- md:setting config.cards_layout_dir -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `layouts` -->

如果您想构建[自定义社交卡片布局][custom layouts]，使用此设置更改存储自定义布局的文件夹，默认为根目录中名为`layouts`的文件夹：

``` yaml
plugins:
  - social:
      cards_layout_dir: layouts
```

提供的路径从根目录解析。

!!! tip "存储自定义布局的位置"

    我们建议将文件夹定位在[`docs`目录][mkdocs.docs_dir]外部，以确保在[构建您的项目]时，您的[自定义布局]不会被复制到[`site`目录][mkdocs.site_dir]中，例如，通过遵循以下目录布局：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    │  └─ *.md
    ├─ layouts/
    │  └─ *.yml
    └─ mkdocs.yml
    ```

---

#### <!-- md:setting config.cards_layout -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `default` -->

插件提供了一系列名为[`default`布局][default layouts]的社交卡片。如果您创建了[自定义社交卡片布局][自定义布局]，您可以指示插件将其用作包含的布局之一：

``` yaml
plugins:
  - social:
      cards_layout: my-custom-layout
```

提供的路径从[`layouts`目录][config.cards_layout_dir]解析。

!!! tip "自定义布局的解析方式"

    默认情况下，插件将从根目录中名为`layouts`的文件夹加载您的[自定义布局]。如果您的布局名为`my-custom-layout`，目录布局必须遵守：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    │  └─ *.md
    ├─ layouts/
    │  └─ my-custom-layout.yml
    └─ mkdocs.yml
    ```

---

#### <!-- md:setting config.cards_layout_options -->

<!-- md:version 9.1.10 -->
<!-- md:default none -->

使用此设置为通过[`cards_layout`][config.cards_layout]指定的布局设置选项（如果布局支持的话），这使得布局可以轻松且完全配置：

``` yaml
plugins:
  - social:
      cards_layout_options:
        <option>: <value>
```

当创建[自定义布局][自定义布局]时，您可以完全自由定义布局的哪些部分可以参数化。插件附带的[`default`布局][default layouts]支持以下选项：

<div class="mdx-columns" markdown>

- [`background_color`][option.background_color]
- [`background_image`][option.background_image]
- [`color`][option.color]
- [`font_family`][option.font_family]
- [`font_variant`][option.font_variant]
- [`logo`][option.logo]
- [`title`][option.title]
- [`description`][option.description]

</div>


  [default layouts]: #layouts

---

#### <!-- md:setting config.cards_include -->

<!-- md:sponsors -->
<!-- md:version insiders-4.35.0 -->
<!-- md:default none -->

使用此设置为项目的子部分启用社交卡片生成，例如，当使用[多个实例]的插件为不同子部分生成不同的社交卡片时：

``` yaml
plugins:
  - social:
      cards_include:
        - blog/*
```

此配置为[`docs`目录][mkdocs.docs_dir]内的`blog`文件夹及其子文件夹中包含的所有页面启用社交卡片生成。

---

#### <!-- md:setting config.cards_exclude -->

<!-- md:sponsors -->
<!-- md:version insiders-4.35.0 -->
<!-- md:default none -->

使用此设置为项目的子部分禁用社交卡片生成，例如，当使用[多个实例]的插件为不同子部分生成不同的社交卡片时：

``` yaml
plugins:
  - social:
      cards_exclude:
        - changelog/*
```

此配置禁用[`docs`目录][mkdocs.docs_dir]内的`changelog`文件夹及其子文件夹中包含的所有页面的社交卡片生成。

### 调试 {#debugging}

插件包括一个用于调试布局的特殊模式，这在创建[自定义布局]时非常有用，因为它允许更快的迭代和更好的理解组合。

以下设置可用于调试：

---

#### <!-- md:setting config.debug -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `false` -->

使用此设置启用用于调试布局的特殊模式，该模式为每个图层渲染带有颜色轮廓的`x`和`y`偏移，并覆盖网格点以进行对齐，从而更容易理解布局的不同层是如何组合在一起的：

``` yaml
plugins:
  - social:
      debug: true
```

---

#### <!-- md:setting config.debug_on_build -->

<!-- md:sponsors -->
<!-- md:version insiders-4.34.1 -->
<!-- md:default `false` -->

默认情况下，插件在[构建您的项目]时自动禁用[`debug`][config.debug]模式，因此您可以确保调试覆盖永远不会部署到生产环境。如果您想更改，请使用：

``` yaml
plugins:
  - social:
      debug_on_build: true
```

I通常不需要更改此设置，因为它只是作为安全网。

---

#### <!-- md:setting config.debug_grid -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `true` -->

当启用[`debug`][config.debug]模式时，此设置指定是否在所有图层上方渲染点网格，以便更好的对齐。如果您想关闭网格，请使用：

``` yaml
plugins:
  - social:
      debug_grid: false
```

---

#### <!-- md:setting config.debug_grid_step -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `32` -->

使用此设置指定启用的网格点的步长（像素），如果启用，这可以帮助创建完美对齐的图层，以实现理想的组合。如果您想更改，请使用：

``` yaml
plugins:
  - social:
      debug_grid_step: 64
```

---

#### <!-- md:setting config.debug_color -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default `grey` -->

使用此设置指定添加到每个图层和在所有图层上方渲染的点网格的轮廓颜色。如果您需要更改，请使用：

``` yaml
plugins:
  - social:
      debug_color: yellow
```

在少数情况下，如果点网格或轮廓难以区分，可能需要更改此设置，因为插件会自动调整颜色，除非显式设置。

## 使用方法 {#usage}

### 元数据 {#metadata}

插件允许通过元数据（前言）覆盖一部分设置，以自定义社交卡片生成，例如，为单个页面或通过利用[meta]插件为整个项目部分设置[包含的`default`布局][default layouts]的[选项]。

以下属性可用：

  [for an entire subsection]: meta.md#how-it-works
  [meta]: meta.md

---

#### <!-- md:setting meta.social.cards -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性覆盖给定页面的[`cards`][config.cards]设置：

``` yaml
---
social:
  cards: false
---

# Page title
...
```

---

#### <!-- md:setting meta.social.cards_layout -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->
<!-- md:flag experimental -->

使用此属性覆盖给定页面的[`cards_layout`][config.cards_layout]设置：

``` yaml
---
social:
  cards_layout: my-custom-layout
---

# Page title
...
```

---

#### <!-- md:setting meta.social.cards_layout_options -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性覆盖给定页面的[`cards_layout_options`][config.cards_layout_options]设置：

``` yaml
---
social:
  cards_layout_options:
    background_color: blue             # Change background color
    background_image: null             # Remove background image
---

# Page title
...
```

设置选项为`#!yaml null`会重置该选项。

### 布局 {#layouts}

虽然构建[自定义布局]是可能且简单的，但插件附带了几种预定义布局，所有这些布局都以`default`为前缀。包括以下布局：

=== "`default`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default
    ```

    <div class="result" markdown>

    ![Layout default]

    此布局设置以下默认值：

    - [`background_color`][option.background_color]
      – <!-- md:default [`theme.palette.primary`][primary color] -->

    - [`font_family`][option.font_family]
      – <!-- md:default [`theme.font.text`][font] -->

    </div>

=== "`default/variant`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/variant
    ```

    <div class="result" markdown>

    ![Layout default variant]

    此布局包括[页面图标]并设置以下默认值：

    - [`background_color`][option.background_color]
      – <!-- md:default [`theme.palette.primary`][primary color] -->

    - [`font_family`][option.font_family]
      – <!-- md:default [`theme.font.text`][font] -->

    </div>

=== "`default/accent`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/accent
    ```

    <div class="result" markdown>

    ![Layout default accent]

    此布局设置以下默认值：

    - [`background_color`][option.background_color]
      – <!-- md:default [`theme.palette.accent`][accent color] -->

    - [`font_family`][option.font_family]
      – <!-- md:default [`theme.font.text`][font] -->

    </div>

=== "`default/invert`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/invert
    ```

    <div class="result" markdown>

    ![Layout default invert]

    此布局设置以下默认值：

    - [`color`][option.background_color]
      – <!-- md:default [`theme.palette.primary`][primary color] -->

    - [`font_family`][option.font_family]
      – <!-- md:default [`theme.font.text`][font] -->

    </div>

=== "`default/only/image`"

    ``` yaml
    plugins:
      - social:
          cards_layout: default/only/image
          cards_layout_options:
            background_image: layouts/background.png

    ```

    <div class="result" markdown>

    此布局仅显示给定的背景图像并将其缩放以覆盖。

    </div>

[`default`布局][default layouts]非常灵活且易于使用，因为它们复制了插件的原始行为，从其他`theme`设置中获取所有选项的默认值。

以下选项可用：

  [Layout default]: ../assets/screenshots/social-cards.png
  [Layout default variant]: ../assets/screenshots/social-cards-variant.png
  [Layout default accent]: ../assets/screenshots/social-cards-accent.png
  [Layout default invert]: ../assets/screenshots/social-cards-invert.png

  [primary color]: ../setup/changing-the-colors.md#primary-color
  [页面图标]: ../reference/index.md#setting-the-page-icon
  [accent color]: ../setup/changing-the-colors.md#accent-color
  [font]: ../setup/changing-the-fonts.md#regular-font

---

#### <!-- md:setting option.background_color -->

<!-- md:version 9.1.10 -->
<!-- md:default computed -->

使用此选项更改生成的社交卡片的背景色。该值可以设置为[pillow支持的有效颜色值]，pillow是用于卡片生成的成像库：

=== "十六进制"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: "#ff1493" # (1)!
    ```

    1.  支持以下表示法，其中`#`后的每个字符必须是`#!css 0-F`范围内的有效十六进制：

        - `#!css #rgb` – 颜色（短）
        - `#!css #rgba` – 颜色+透明度（短）
        - `#!css #rrggbb` – 颜色
        - `#!css #rrggbbaa` – 颜色+透明度

=== "颜色函数"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: rgb(255, 20, 147) # (1)!
    ```

    1.  支持以下函数，列出了允许的最大值，最小值都是`#!css 0`或`#!css 0%`：

        - `#!css rgb(255, 255, 255)` – 红、绿、蓝
        - `#!css hsl(360, 100%, 100%)` – 色调、饱和度和亮度
        - `#!css hsv(360, 100%, 100%)` – 色调、饱和度和值

=== "颜色名称"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_color: deeppink # (1)!
    ```

    1.  请参阅[`<named-color>`][named-color] CSS数据类型的支持颜色名称列表。注意，有些可能不可用。

如果此选项与[`background_image`][option.background_image]一起使用，颜色将在图像上方渲染，允许对图像进行着色。如果您想移除背景色，请使用：

``` yaml
plugins:
  - social:
      cards_layout_options:
        background_color: transparent
```

  [pillow支持的有效颜色值]: https://pillow.readthedocs.io/en/stable/reference/ImageColor.html#color-names
  [named-color]: https://developer.mozilla.org/en-US/docs/Web/CSS/named-color

---

#### <!-- md:setting option.background_image -->

<!-- md:sponsors -->
<!-- md:version insiders-4.33.0 -->
<!-- md:default none -->

使用此选项为生成的社交卡片定义背景图像。请注意，图像将与[`background_color`][option.background_color]一起染色，后者也可以设置为`transparent`：

=== "图像"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_image: layouts/background.png
            background_color: transparent
    ```

=== "带着色的图像"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            background_image: layouts/background.png
            background_color: "#ff149366"
    ```

提供的路径从根目录解析。

---

#### <!-- md:setting option.color -->

<!-- md:version 9.1.10 -->
<!-- md:default computed -->

使用此选项更改生成的社交卡片的前景色。该值可以设置为[pillow支持的有效颜色值]，pillow是用于卡片生成的成像库：

=== "十六进制"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: "#ffffff" # (1)!
    ```

    1.  支持以下表示法，其中`#`后的每个字符必须是`#!css 0-F`范围内的有效十六进制：

        - `#!css #rgb` – 颜色（短）
        - `#!css #rgba` – 颜色+透明度（短）
        - `#!css #rrggbb` – 颜色
        - `#!css #rrggbbaa` – 颜色+透明度

=== "颜色函数"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: rgb(255, 255, 255) # (1)!
    ```

    1.  支持以下函数，列出了允许的最大值，最小值都是`#!css 0`或`#!css 0%`：

        - `#!css rgb(255, 255, 255)` – 红、绿、蓝
        - `#!css hsl(360, 100%, 100%)` – 色调、饱和度和亮度
        - `#!css hsv(360, 100%, 100%)` – 色调、饱和度和值

=== "颜色名称"

    ``` yaml
    plugins:
      - social:
          cards_layout_options:
            color: white # (1)!
    ```

    1.  请参阅[`<named-color>`][named-color] CSS数据类型的支持颜色名称列表。注意，有些可能不可用。

---

#### <!-- md:setting option.font_family -->

<!-- md:version 9.1.10 -->
<!-- md:default computed -->

使用此选项更改生成的社交卡片的字体家族。插件会自动从[Google Fonts]下载字体，因此字体必须指向一个存在的Google字体：

``` yaml
plugins:
  - social:
      cards_layout_options:
        font_family: Ubuntu
```

当您在[Google Fonts]上找到一个您喜欢的字体时，您只需从字体的样本页面复制名称并将其用作此选项的值——无需进一步配置。

  [Google Fonts]: https://fonts.google.com/

---

#### <!-- md:setting option.font_variant -->

<!-- md:sponsors -->
<!-- md:version insiders-4.53.3 -->
<!-- md:default none -->

使用此选项更改用于生成社交卡片的字体变体。如果下载的字体具有如`Condensed`或`Expanded`等变体，您可以设置它们：

``` yaml
plugins:
  - social:
      cards_layout_options:
        font_variant: Condensed
```

变体与自定义布局中使用的样式组合，因此插件被指示使用像`Condensed Regular`或`Expanded Bold`这样的组合。

---

#### <!-- md:setting option.logo -->

<!-- md:sponsors -->
<!-- md:version insiders-4.40.0 -->
<!-- md:default computed -->

使用此选项更改用于生成社交卡片的徽标。默认情况下，插件使用[`theme.logo`][theme.logo]或[`theme.icon.logo`][theme.icon.logo]设置，这些设置来自`mkdocs.yml`。您可以更改它：

``` yaml
plugins:
  - social:
      cards_layout_options:
        logo: layouts/logo.png
```

提供的路径从根目录解析。

  [theme.logo]: ../setup/changing-the-logo-and-icons.md#logo-image
  [theme.icon.logo]: ../setup/changing-the-logo-and-icons.md#logo-icon-bundled

---

#### <!-- md:setting option.title -->

<!-- md:sponsors -->
<!-- md:version insiders-4.40.0 -->
<!-- md:default computed -->

使用此选项更改生成的社交卡片的标题。这将覆盖由MkDocs分配的计算页面标题，以及[`title`][meta.title]元数据属性：

``` yaml
plugins:
  - social:
      cards_layout_options:
        title: My custom title
```

  [meta.title]: ../reference/index.md#setting-the-page-title

---

#### <!-- md:setting option.description -->

<!-- md:sponsors -->
<!-- md:version insiders-4.40.0 -->
<!-- md:default computed -->

使用此选项更改生成的社交卡片的描述。这将覆盖已设置的[`site_description`][mkdocs.site_description]（如果定义），以及[`description`][meta.description]元数据属性：

``` yaml
plugins:
  - social:
      cards_layout_options:
        description: My custom description
```

  [meta.description]: ../reference/index.md#setting-the-page-description

---

!!! question "缺少某些功能？"

    在设置社交卡片时，您可能会发现缺少特定功能——我们乐意考虑将其添加到插件中！您可以[开启一个讨论]来提出问题，或在我们的[问题追踪器]上创建一个[变更请求]，以便我们了解它是否适合插件。

  [开启一个讨论]: https://github.com/squidfunk/mkdocs-material/discussions
  [变更请求]: ../contributing/requesting-a-change.md
  [问题追踪器]: https://github.com/squidfunk/mkdocs-material/issues
