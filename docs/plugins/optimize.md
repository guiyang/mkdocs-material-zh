---
title: 内置优化插件
icon: material/rabbit
---

# 内置优化插件 {#built-in-optimize-plugin}

优化插件在[构建您的项目]时自动识别并优化所有媒体文件，使用常见的压缩和转换技术。因此，您的站点加载速度显著加快，并在搜索引擎中获得更好的排名。

---

<!-- md:sponsors --> __仅限赞助者__ — 此插件目前仅供[我们的优秀赞助者]使用。

  [构建您的项目]: ../creating-your-site.md#building-your-site
  [我们的优秀赞助者]: ../insiders/index.md

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件扫描[`docs`目录][mkdocs.docs_dir]中的媒体文件和资产，并自动优化它们以减少[`site`目录][mkdocs.site_dir]的最终大小。这导致加载时间更快，因为您向用户发送的字节更少，同时还为[离线可用文档]提供了更小的下载。

优化后的图像采用[智能缓存][智能缓存]，这就是为什么插件只优化自上次构建以来发生变化的媒体文件。这使得更换或更新图像变得可能，无需担心优化它们，更糟的是，忘记这么做。

为了优化媒体文件，您的系统上需要有一些[依赖项]。

  [离线可用文档]: ../setup/building-for-offline-usage.md
  [依赖项]: #configuration

### 何时使用它 {#when-to-use-it}

通常建议使用该插件，因为媒体文件会自动优化，无需干预，确保您的站点尽可能快地加载。优化后的媒体文件是搜索引擎中高排名和持续排名的关键组成部分。

此外，该插件可以与 Material for MkDocs 提供的其他内置插件结合使用，以创建针对您项目的复杂构建管道：

<div class="grid cards" markdown>

-   :material-shield-account: &nbsp; __[内置隐私插件][privacy]__

    ---

    隐私插件使使用未优化的外部资产变得简单，将它们传递给优化插件，然后复制到[`site`目录][mkdocs.site_dir]。

    ---

    __外部媒体文件可以自动下载并优化__

-   :material-connection: &nbsp; __[内置离线插件][offline]__

    ---

    离线插件增加了构建离线可用文档的支持，因此您可以将[`site`目录][mkdocs.site_dir]分发为可下载的`.zip`文件。

    ---

    __您的文档可以作为更小的`.zip`文件分发__

</div>

  [privacy]: privacy.md
  [offline]: offline.md

## 配置 {#configuration}

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:plugin [optimize] – built-in -->
<!-- md:flag multiple -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用优化插件非常简单。只需将以下行添加到`mkdocs.yml`，并观察媒体文件如何自动优化：

``` yaml
plugins:
  - optimize
```

优化插件已内置于 Material for MkDocs 中，无需安装。

不过，为了优化所有媒体文件，如果您的系统上还没有安装[图像处理]的依赖，需要安装它们。链接的指南包括了几个操作系统的说明，并提到了一些替代环境。

  [optimize]: optimize.md
  [内置插件]: index.md
  [图像处理]: requirements/image-processing.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。如果您想禁用插件，例如，对于本地构建，您可以在`mkdocs.yml`中使用[环境变量][mkdocs.env]：

``` yaml
plugins:
  - optimize:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

---

#### <!-- md:setting config.concurrency -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default available CPUs - 1 -->

拥有更多 CPU 可用时，插件可以并行处理更多工作，从而更快完成媒体文件优化。如果您想完全禁用并发处理，请使用：

``` yaml
plugins:
  - optimize:
      concurrency: 1
```

默认情况下，插件使用所有可用的 CPU 减 1，最少为 1。

### 缓存 {#caching}

插件实现了一个[智能缓存]机制，确保只有在媒体文件或资产内容发生变化时，才会通过优化管道传递。如果您更换或更新了图像，插件会检测到并更新媒体文件的优化版本。

以下设置适用于缓存：

  [智能缓存]: requirements/caching.md

---

#### <!-- md:setting config.cache -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置指示插件绕过缓存，以便重新优化所有媒体文件，即使缓存可能不是陈旧的。通常不需要指定此设置，除非是在调试插件本身时。可以通过以下方式禁用缓存：

``` yaml
plugins:
  - optimize:
      cache: false
```

---

#### <!-- md:setting config.cache_dir -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `.cache/plugin/optimize` -->

通常不需要指定此设置，除非您想更改媒体文件缓存的根目录路径。如果您想更改它，请使用：

``` yaml
plugins:
  - optimize:
      cache_dir: my/custom/dir
```

如果您正在使用[多个实例]的插件，将不同的缓存目录设置为不同的实例可能是个好主意，这样它们就不会相互干扰。

  [多个实例]: index.md#multiple-instances

### 优化 {#optimization}

文档通常使用截图或图表来更好地可视化事物，这两者都是优化的首选对象。插件自动使用[pngquant]优化`.png`文件，使用[Pillow]优化`.jpg`文件。

以下设置适用于优化：

  [pngquant]: https://pngquant.org/
  [Pillow]: https://pillow.readthedocs.io/

---

#### <!-- md:setting config.optimize -->

<!-- md:sponsors -->
<!-- md:version insiders-4.41.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用媒体文件优化。目前，插件的唯一目的是优化媒体文件，所以它相当于[`enabled`][config.enabled]设置，但在不久的将来，可能会添加其他功能。如果您想禁用优化，请使用：

``` yaml
plugins:
  - optimize:
      optimize: false
```

---

#### <!-- md:setting config.optimize_png -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用`.png`文件的优化。通常不需要指定此设置，但如果您想禁用`.png`文件的优化，请使用：

``` yaml
plugins:
  - optimize:
      optimize_png: false
```

---

#### <!-- md:setting config.optimize_png_speed -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `3` of `1-10` -->

使用此设置来指定 [pngquant] 在优化 `.png` 文件时应用的速度/质量折衷。数字越低，[pngquant] 优化得越激进：

=== "更慢 <small>更小</small>"

    ``` yaml
    plugins:
      - optimize:
          optimize_png_speed: 1
    ```

=== "更快 <small>更大</small>"

    ``` yaml
    plugins:
      - optimize:
          optimize_png_speed: 10
    ```

`10` 的因子质量降低 5%，但比默认的 `3` 快 8 倍。

---

#### <!-- md:setting config.optimize_png_strip -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置指定 [pngquant] 是否应剥离 `.png` 文件中不需要显示图像的可选元数据，例如，[EXIF]。
如果您想保留元数据，请使用：

``` yaml
plugins:
  - optimize:
      optimize_png_strip: false
```

  [EXIF]: https://en.wikipedia.org/wiki/Exif

---

#### <!-- md:setting config.optimize_jpg -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用 `.jpg` 文件的优化。通常不需要指定此设置，但如果您想禁用 `.jpg` 文件的优化，请使用：

``` yaml
plugins:
  - optimize:
      optimize_jpg: false
```

---

#### <!-- md:setting config.optimize_jpg_quality -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `60` of `0-100` -->

使用此设置指定 [Pillow] 在优化 `.jpg` 文件时应用的图像质量。如果图像看起来模糊，调整并更改此设置是个好主意：

``` yaml
plugins:
  - optimize:
      optimize_jpg_quality: 75
```

---

#### <!-- md:setting config.optimize_jpg_progressive -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置指定 [Pillow] 在优化 `.jpg` 文件时是否应使用渐进式编码，以便在慢速连接上更快地呈现。如果您想禁用渐进式编码，请使用：

``` yaml
plugins:
  - optimize:
      optimize_jpg_progressive: false
```

  [progressive encoding]: https://medium.com/hd-pro/jpeg-formats-progressive-vs-baseline-73b3938c2339

---

#### <!-- md:setting config.optimize_include -->

<!-- md:sponsors -->
<!-- md:version insiders-4.41.0 -->
<!-- md:default none -->

使用此设置为项目的特定目录启用媒体文件优化，例如，当使用 [多个实例] 的插件以不同方式优化媒体文件时：

``` yaml
plugins:
  - optimize:
      optimize_include:
        - screenshots/*
```

此配置为 [`docs` 目录][mkdocs.docs_dir] 内的 `screenshots` 文件夹及其子文件夹中包含的所有媒体文件启用优化。

---

#### <!-- md:setting config.optimize_exclude -->

<!-- md:sponsors -->
<!-- md:version insiders-4.41.0 -->
<!-- md:default none -->

使用此设置为项目的特定目录禁用媒体文件优化，例如，当使用 [多个实例] 的插件以不同方式优化媒体文件时：

``` yaml
plugins:
  - social:
      optimize_exclude:
        - vendor/*
```

此配置禁用 [`docs` 目录][mkdocs.docs_dir] 内的 `vendor` 文件夹及其子文件夹中包含的所有媒体文件的优化。

### 报告 {#reporting}

以下设置可用于报告：

---

#### <!-- md:setting config.print_gain -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应在优化每个文件后打印获得的字节数。如果您想禁用此行为，请使用：

``` yaml
plugins:
  - optimize:
      print_gain: false
```

---

#### <!-- md:setting config.print_gain_summary -->

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应在优化所有文件后打印总获得的字节数。如果您想禁用此行为，请使用：

``` yaml
plugins:
  - optimize:
      print_gain_summary: false
```
