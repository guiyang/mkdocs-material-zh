# 确保数据隐私 {#ensuring-data-privacy}

Material for MkDocs 使得遵守数据隐私法规变得非常简单，因为它提供了原生的[Cookie 同意]解决方案，在设置[分析]之前寻求用户的明确同意。此外，外部资产可以自动下载，用于[自托管]。

  [Cookie 同意]: #cookie-consent
  [分析]: setting-up-site-analytics.md
  [自托管]: #built-in-privacy-plugin

## 配置 {#configuration}

### Cookie 同意 {#cookie-consent}

<!-- md:version 8.4.0 -->
<!-- md:default none -->
<!-- md:flag experimental -->
<!-- md:example cookie-consent -->

Material for MkDocs 提供了一个原生且可扩展的 Cookie 同意表单，在向第三方发送请求之前询问用户的同意。在 `mkdocs.yml` 中添加以下内容：

``` yaml
extra:
  consent:
    title: Cookie consent
    description: >- # (1)!
      We use cookies to recognize your repeated visits and preferences, as well
      as to measure the effectiveness of our documentation and whether users
      find what they're searching for. With your consent, you're helping us to
      make our documentation better.
```

1.  您可以在 `description` 中添加任意 HTML 标签，例如链接到您的服务条款或站点的其他部分。

以下属性可用：

<!-- md:option consent.title -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性设置 Cookie 同意的标题，显示在表单顶部，必须设置为非空字符串。

<!-- md:option consent.description -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性设置 Cookie 同意的描述，显示在标题下方，可以包含原始 HTML（例如，链接到服务条款）。

<!-- md:option consent.cookies -->

:   <!-- md:default none --> This property allows to add custom
    cookies 或更改内置 cookies 的初始“选中”状态和名称。目前，以下 cookies 是内置的：

    - __谷歌分析__ – `analytics`（默认启用）
    - __GitHub__ – `github`（默认启用）

    每个 cookie 必须接收一个用作 `cookies` 映射中键的唯一标识符，并且可以设置为字符串，或者为定义 `name` 和 `checked` 状态的映射：

    ===  "自定义 cookie 名称"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics: Custom name
        ```

    ===  "自定义初始状态"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics:
                name: Google Analytics
                checked: false
        ```

    ===  "自定义 cookie"

        ``` yaml
        extra:
          consent:
            cookies:
              analytics: Google Analytics # (1)!
              custom: Custom cookie
        ```

        1.  如果您在 `cookies` 属性中定义了一个自定义 cookie，必须显式添加回 `analytics` cookie，否则不会触发分析。

    如果通过 `mkdocs.yml` 配置了谷歌分析，cookie 同意将自动包括一个用户禁用它的设置。[自定义 cookies] 可以在 JavaScript 中使用。

<!-- md:option consent.actions -->

:   <!-- md:default `[accept, manage]` --> This property defines
    显示哪些按钮以及顺序，例如，允许用户接受 cookies 并管理设置：

    ``` yaml
    extra:
      consent:
        actions:
          - accept
          - manage # (1)!
    ```

    1.  如果从 `actions` 属性中省略了 `manage` 设置按钮，设置始终显示。

    Cookie 同意表单包括三种类型的按钮：

    - `accept` – 接受选定 cookies 的按钮
    - `reject` – 拒绝所有 cookies 的按钮
    - `manage` – 管理设置的按钮

当用户首次访问您的网站时，会显示一个 Cookie 同意表单：

[![Cookie consent enabled]][Cookie consent enabled]

  [自定义 cookies]: #custom-cookies
  [Cookie consent enabled]: ../assets/screenshots/consent.png

#### 更改 Cookie 设置 {#change-cookie-settings}

为了符合 GDPR，用户必须随时能够更改他们的 Cookie 设置。这可以通过在 `mkdocs.yml` 中添加一个简单的链接到您的[版权声明]来完成：

``` yaml
copyright: >
  Copyright &copy; 2016 - 2024 Martin Donath –
  <a href="#__consent">Change cookie settings</a>
```

  [版权声明]: setting-up-the-footer.md#copyright-notice

### 内置隐私插件 {#built-in-privacy-plugin}

<!-- md:version 9.5.0 -->
<!-- md:plugin [privacy][built-in privacy plugin] -->
<!-- md:flag experimental -->

内置隐私插件在构建过程中自动识别外部资产，并下载所有资产以便非常简单的自托管。在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - privacy
```

有关所有设置的列表，请参阅[插件文档]。

  [插件文档]: ../plugins/privacy.md

!!! tip "外部托管图像并自动优化它们"

    当您想要在 git 仓库之外的其他位置托管资产如图像，以保持它们的新鲜度和您的仓库精简时，这个选项使得[内置隐私插件]成为一个极佳的选择。

    此外，截至 <!-- md:version insiders-4.30.0 -->，内置隐私插件已经完全重写，现在与[内置优化插件]完美协作，这意味着外部资产可以通过与您的文档其余部分相同的优化流程传递。这意味着您可以在仓库外存储和编辑未优化的文件，并让这两个插件为您构建一个高度优化的网站。

    如果您想实现单独的管道，即对某些图像进行不同的优化，或者从下载中排除某些图像，您可以使用[内置隐私插件]的多个实例。

!!! question "为什么 Material for MkDocs 不能按设计捆绑所有资产？"

    Material for MkDocs 不能仅仅捆绑自己的所有资产的主要原因是与[谷歌字体]的集成，它提供了超过一千种不同的字体，可用于渲染您的文档。大多数字体包括几种权重，并分为不同的字符集以保持下载大小小，因此浏览器只下载真正需要的内容。对于我们的默认[常规字体] Roboto，这总共结果在 [42 个 `*.woff2` 文件][example]。

    如果 Material for MkDocs 捆绑所有字体文件，下载大小将达到数百兆字节，减慢自动构建的速度。此外，作者可能会添加外部资产，如第三方脚本或样式表，这些需要记住定义为更多的本地资产。

    这正是[内置隐私插件]存在的原因——它自动化了手动下载所有外部资产的过程，以确保符合 GDPR，尽管存在一些[技术限制]。

  [谷歌字体]: changing-the-fonts.md
  [常规字体]: changing-the-fonts.md#regular-font
  [example]: #example
  [内置优化插件]: ../plugins/optimize.md

??? example "展开查看示例"

    对于官方文档，[内置隐私插件]下载了以下资源：

    ``` { .sh .no-copy #example }
    .
    └─ assets/external/
       ├─ unpkg.com/tablesort@5.3.0/dist/tablesort.min.js
       ├─ fonts.googleapis.com/css
       ├─ fonts.gstatic.com/s/
       │  ├─ roboto/v29/
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc-CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc0CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc1CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc2CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc3CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc5CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TjASc6CsQ.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic-CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic0CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic1CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic2CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic3CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic5CsTKlA.woff2
       │  │  ├─ KFOjCnqEu92Fr1Mu51TzBic6CsQ.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xEIzIFKw.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xFIzIFKw.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xGIzIFKw.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xHIzIFKw.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xIIzI.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xLIzIFKw.woff2
       │  │  ├─ KFOkCnqEu92Fr1Mu51xMIzIFKw.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fABc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fBBc4.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fBxc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fCBc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fCRc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fChc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmSU5fCxc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfABc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfBBc4.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfBxc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfCBc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfCRc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfChc4EsA.woff2
       │  │  ├─ KFOlCnqEu92Fr1MmWUlfCxc4EsA.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu4WxKOzY.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu4mxK.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu5mxKOzY.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu72xKOzY.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu7GxKOzY.woff2
       │  │  ├─ KFOmCnqEu92Fr1Mu7WxKOzY.woff2
       │  │  └─ KFOmCnqEu92Fr1Mu7mxKOzY.woff2
       │  └─ robotomono/v13/
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSV0mf0h.woff2
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSZ0mf0h.woff2
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSd0mf0h.woff2
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSh0mQ.woff2
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSt0mf0h.woff2
       │     ├─ L0xTDF4xlVMF-BfR8bXMIhJHg45mwgGEFl0_3vrtSM1J-gEPT5Ese6hmHSx0mf0h.woff2
       │     ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtElOUlYIw.woff2
       │     ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEleUlYIw.woff2
       │     ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEluUlYIw.woff2
       │     ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEm-Ul.woff2
       │     ├─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEmOUlYIw.woff2
       │     └─ L0xdDF4xlVMF-BfR8bXMIjhOsXG-q2oeuFoqFrlnAIe2Imhk1T8rbociImtEn-UlYIw.woff2
       └─ polyfill.io/v3/polyfill.min.js
    ```

  [内置隐私插件]: ../plugins/privacy.md
  [preconnect]: https://developer.mozilla.org/en-US/docs/Web/Performance/dns-prefetch

#### 高级设置 {#advanced-settings}

<!-- md:sponsors -->
<!-- md:version insiders-4.50.0 -->

以下高级设置目前仅限我们的[赞助商][Insiders]。它们完全是可选的，并且不影响博客的功能，但对于定制可能有帮助：

- [`log`][config.log]
- [`log_level`][config.log_level]

随着我们发现新的用例，我们将在这里添加更多设置。

  [Insiders]: ../insiders/index.md
  [config.log]: ../plugins/privacy.md#config.log
  [config.log_level]: ../plugins/privacy.md#config.log_level

## 自定义 {#customization}

### 自定义 cookies {#custom-cookies}

<!-- md:version 8.4.0 -->
<!-- md:example custom-cookies -->

如果您自定义了[Cookie 同意]并添加了一个`自定义`cookie，用户将被提示接受或拒绝您的自定义 cookie。一旦用户接受或拒绝 Cookie 同意，或者[更改设置]，页面将重新加载[^1]。使用[额外的 JavaScript]查询结果：

  [^1]:
    我们重新加载页面是为了使与自定义 cookies 的互操作更简单。如果 Material for MkDocs 实现了基于回调的方法，作者将需要确保正确更新使用 cookies 的所有脚本。此外，Cookie 同意最初只回答一次，这就是为什么我们认为这是 DX 和 UX 的一个好的权衡。

=== ":octicons-file-code-16: `docs/javascripts/consent.js`"

    ``` js
    var consent = __md_get("__consent")
    if (consent && consent.custom) {
      /* The user accepted the cookie */
    } else {
      /* The user rejected the cookie */
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/consent.js
    ```

  [额外的 JavaScript]: ../customization.md#additional-javascript
  [changes the settings]: #change-cookie-settings
