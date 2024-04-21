---
title: 内置隐私插件
icon: material/shield-account
---

# 内置隐私插件 {#built-in-privacy-plugin}

隐私插件提供了一个流畅的解决方案，用于自动托管外部资源。仅通过一行配置，插件就可以自动识别并下载外部资源，使得遵守GDPR（通用数据保护条例）变得尽可能简单。

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件扫描生成的HTML以寻找外部资源，即脚本、样式表、图片和网络字体，下载它们，将它们存储在[`site`目录][mkdocs.site_dir]中，并替换所有引用为指向下载副本的链接，从而轻松自托管。例如：

``` html
<script src="https://example.com/script.js"></script>
```

这个外部脚本被下载，链接被替换为：

``` html
<script src="assets/external/example.com/script.js"></script>
```

当然，脚本和样式表可以引用更多外部资源，这就是为什么这个过程会递归重复，直到不再检测到外部资源为止：

- 脚本会被扫描以寻找更多的脚本、样式表和JSON文件
- 样式表会被扫描以寻找图片和网络字体

此外，像[`preconnect`][preconnect]这样的提示，用于减少请求外部资源的延迟，也会从输出中删除，因为在自托管时不需要它们。插件完成工作后，您的项目将不会请求外部服务。

有一些[限制]。

  [preconnect]: https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/preconnect
  [限制]: #limitations

### 何时使用它 {#when-to-use-it}

该插件的开发是为了使遵守2018年欧洲 __通用数据保护条例__（GDPR）尽可能简单，同时保留Material for MkDocs提供的灵活性和功能，例如其与[Google Fonts]的紧密集成。

但这只是开始。例如，如果您的项目包含许多图片，启用插件可以将它们从您的存储库中移出，因为插件将在[构建您的项目]时自动下载并存储它们在[`site`目录][mkdocs.site_dir]中。

更有趣的是，该插件可以与Material for MkDocs提供的其他内置插件组合使用，以创建针对您的项目的复杂构建管道：

<div class="grid cards" markdown>

-   :material-rabbit: &nbsp; __[内置优化插件][optimize]__

    ---

    优化插件允许优化隐私插件检测到的所有下载的外部资源，使用压缩和转换技术。

    ---

    __外部媒体文件自动下载并优化__

-   :material-connection: &nbsp; __[内置离线插件][offline]__

    ---

    离线插件增加了构建[离线可用文档]的支持，因此您可以将[`site`目录][mkdocs.site_dir]作为可下载的`.zip`文件分发。

    ---

    __您的文档可以在没有互联网连接的情况下工作__

</div>

  [Google Fonts]: ../setup/changing-the-fonts.md
  [构建您的项目]: ../creating-your-site.md#building-your-site
  [optimize]: optimize.md
  [offline]: offline.md
  [离线可用文档]: ../setup/building-for-offline-usage.md

## 配置 {#configuration}

<!-- md:version 9.5.0 -->
<!-- md:plugin [privacy] – built-in -->
<!-- md:flag multiple -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用隐私插件非常简单。只需将以下行添加到`mkdocs.yml`，并开始轻松自托管外部资源：

``` yaml
plugins:
  - privacy
```

隐私插件已内置于Material for MkDocs中，无需安装。

  [privacy]: privacy.md
  [内置插件]: index.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.5.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。如果您想禁用插件，例如，对于本地构建，您可以在`mkdocs.yml`中使用[环境变量][mkdocs.env]：

``` yaml
plugins:
  - privacy:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

---

#### <!-- md:setting config.concurrency -->

<!-- md:version 9.5.0 -->
<!-- md:default available CPUs - 1 -->

有更多的CPU可用时，插件可以并行处理更多工作，从而更快地完成外部资产的处理。如果您想完全禁用并发处理，请使用：

``` yaml
plugins:
  - privacy:
      concurrency: 1
```

默认情况下，插件使用所有可用的CPU - 1，最少为1。

### 缓存 {#caching}

插件实现了一个[智能缓存]机制，确保只有在缓存中不存在时才下载外部资产。虽然初始构建可能需要一些时间，但使用缓存是个好主意，因为它会加快连续构建的速度。

以下设置可用于缓存：

  [智能缓存]: requirements/caching.md

---

#### <!-- md:setting config.cache -->

<!-- md:version 9.5.0 -->
<!-- md:default `true` -->

使用此设置指示插件绕过缓存，以重新安排所有外部资产的下载，即使缓存可能并未过期。通常不需要指定此设置，除非在调试插件本身时。可以使用以下方法禁用缓存：

``` yaml
plugins:
  - privacy:
      cache: false
```

---

#### <!-- md:setting config.cache_dir -->

<!-- md:version 9.5.0 -->
<!-- md:default `.cache/plugin/privacy` -->

通常不需要指定此设置，除非您想更改根目录内下载副本缓存的路径。如果您想更改它，请使用：

``` yaml
plugins:
  - privacy:
      cache_dir: my/custom/dir
```

如果您正在使用插件的[多个实例]，为每个实例设置不同的缓存目录可能是个好主意，这样它们就不会相互干扰。

  [多个实例]: index.md#multiple-instances

### 日志记录 {#logging}

以下设置可用于日志记录：

---

#### <!-- md:setting config.log -->

<!-- md:sponsors -->
<!-- md:version insiders-4.50.0 -->
<!-- md:default `true` -->

使用此设置控制插件在构建站点时是否显示日志消息。虽然不推荐，但您可以禁用日志记录：

``` yaml
plugins:
  - privacy:
      log: false
```

---

#### <!-- md:setting config.log_level -->

<!-- md:sponsors -->
<!-- md:version insiders-4.50.0 -->
<!-- md:default `info` -->

使用此设置控制插件在遇到错误时应使用的日志级别，这要求启用[`log`][config.log]设置。以下日志级别可用：

=== "`error`"

    ``` yaml
    plugins:
      - privacy:
          log_level: error
    ```

    仅报告错误。

=== "`warn`"

    ``` yaml
    plugins:
      - privacy:
          log_level: warn
    ```

    报告错误和警告，在[`strict`][mkdocs.strict]模式下终止构建。这包括当无法在Windows系统上创建符号链接(#6550)时的警告。

=== "`info`"

    ``` yaml
    plugins:
      - privacy:
          log_level: info
    ```

    报告错误、警告和信息性消息，包括插件成功下载哪些资产。

=== "`debug`"

    ``` yaml
    plugins:
      - privacy:
          log_level: debug
    ```

    报告所有消息，包括调试消息，前提是MkDocs是用`--verbose`标志启动的。请注意，这将打印大量消息，仅用于调试。

### 外部资产 {#external-assets}

以下设置可用于外部资产：

---

#### <!-- md:setting config.assets -->

<!-- md:version 9.5.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应下载外部资产。如果您只希望插件处理[外部链接]，您可以禁用外部资产的处理：

``` yaml
plugins:
  - privacy:
      assets: false
```

  [外部链接]: #external-links

---

#### <!-- md:setting config.assets_fetch -->

<!-- md:version 9.5.0 -->
<!-- md:default `true` -->

使用此设置控制插件在遇到外部资产时是否应下载或仅报告外部资产。如果您已经自行托管所有外部资产，此设置可用作安全网，以检测作者在页面中放置的指向外部资产的链接：

``` yaml
plugins:
  - privacy:
      assets_fetch: true
```

---

#### <!-- md:setting config.assets_fetch_dir -->

<!-- md:version 9.5.0 -->
<!-- md:default `assets/external` -->

通常不需要指定此设置，除非您想更改[`site`目录][mkdocs.site_dir]内存储外部资产的路径。如果您想更改它，请使用：

``` yaml
plugins:
  - privacy:
      assets_fetch_dir: my/custom/dir
```

此配置将下载的副本存储在[`site`目录][mkdocs.site_dir]的`my/custom/dir`中。

---

#### <!-- md:setting config.assets_include -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:default none -->

使用此设置为特定来源启用下载外部资产，例如，当使用插件的[多个实例]以针对不同来源微调外部资产的处理时：

``` yaml
plugins:
  - privacy:
      assets_include:
        - unsplash.com/*
```

---

#### <!-- md:setting config.assets_exclude -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:default none -->

使用此设置为特定来源禁用下载外部资产，例如，当使用插件的[多个实例]以针对不同来源微调外部资产的处理时：

``` yaml
plugins:
  - privacy:
      assets_exclude: # (1)!
        - cdn.jsdelivr.net/npm/mathjax@3/*
        - giscus.app/*
```

1.  [MathJax]加载用于数学内容排版的网络字体通过相对URL，因此不能由隐私插件自动捆绑。[MathJax可以自托管]。

    [Giscus]，我们推荐用作[评论系统]，使用称为代码分割的技术来只加载必要的代码，这是通过相对URL实现的。[Giscus也可以自托管]。

  [MathJax]: ../reference/math.md
  [MathJax可以自托管]: https://docs.mathjax.org/en/latest/web/hosting.html
  [Giscus]: https://giscus.app/
  [评论系统]: ../setup/adding-a-comment-system.md
  [Giscus也可以自托管]: https://github.com/giscus/giscus/blob/main/SELF-HOSTING.md

---

### 外部链接 {#external-links}

以下设置可用于外部链接：

---

#### <!-- md:setting config.links -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:default `true` -->

使用此设置指示插件解析并处理外部链接，以便为其添加注释以[提高安全性]，或自动向外部链接添加额外属性。如果您想禁用外部链接的处理，请使用：

``` yaml
plugins:
  - privacy:
      links: false
```

  [提高安全性]: https://developer.chrome.com/en/docs/lighthouse/best-practices/external-anchors-use-rel-noopener/

---

#### <!-- md:setting config.links_attr_map -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:default none -->

使用此设置指定应添加到外部链接的额外属性，例如，为所有外部链接添加`target="_blank"`，使它们在新标签页中打开：

``` yaml
plugins:
  - privacy:
      links_attr_map:
        target: _blank
```

---

#### <!-- md:setting config.links_noopener -->

<!-- md:sponsors -->
<!-- md:version insiders-4.37.0 -->
<!-- md:default `true` -->

通常不建议更改此设置，因为它会自动为在新窗口中打开的外部链接添加`rel="noopener"`以[提高安全性]：

``` yaml
plugins:
  - privacy:
      links_noopener: true
```

## 限制 {#limitations}

动态创建的URL作为脚本的一部分不会被检测到，因此不能自动下载，因为插件不执行脚本——它只检测用于下载和替换的完全限定URL。简而言之，不要这样做：

``` js
const cdn = "https://polyfill.io"
const url = `${cdn}/v3/polyfill.min.js`
```

相反，始终使用完全限定的URL：

``` js
const url ="https://polyfill.io/v3/polyfill.min.js"
```
