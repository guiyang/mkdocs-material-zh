# 更改字体 {#changing-the-fonts}

Material for MkDocs 使得更改项目文档的字体变得简单，因为它直接集成了 [Google 字体]。或者，如果出于数据隐私原因更喜欢自托管字体或使用其他来源，则可以自定义加载字体。

  [Google 字体]: https://fonts.google.com

## 配置 {#configuration}

### 常规字体 {#regular-font}

<!-- md:version 0.1.2 -->
<!-- md:default [`Roboto`][Roboto] -->

常规字体用于所有正文、标题以及基本上不需要等宽字体的内容。可以通过 `mkdocs.yml` 设置任何有效的 [Google Font][Google Fonts]：

``` yaml
theme:
  font:
    text: Roboto
```

字体将以 300、400、_400i_ 和 __700__ 的格式加载。

  [Roboto]: https://fonts.google.com/specimen/Roboto

### 等宽字体 {#monospaced-font}

<!-- md:version 0.1.2 -->
<!-- md:default [`Roboto Mono`][Roboto Mono] -->

_等宽字体_ 用于代码块，并且可以单独配置。就像常规字体一样，它可以通过 `mkdocs.yml` 设置任何有效的 [Google 字体][Google 字体]：

``` yaml
theme:
  font:
    code: Roboto Mono
```

字体将以 400 的格式加载。

  [Roboto Mono]: https://fonts.google.com/specimen/Roboto+Mono

### 自动加载 {#autoloading}

<!-- md:version 1.0.0 -->
<!-- md:default none -->

如果你想阻止从 [Google 字体] 加载字体，例如遵守 [数据隐私] 法规，并回退到系统字体，请添加以下行到 `mkdocs.yml` 中：

``` yaml
theme:
  font: false
```

!!! tip "自动捆绑 Google 字体"

    [内置隐私插件] 使得使用 Google 字体同时符合 __通用数据保护条例__ (GDPR) 变得简单，通过自动下载并自托管网页字体文件。

  [数据隐私]: https://developers.google.com/fonts/faq/privacy
  [内置隐私插件]:../plugins/privacy.md

## 自定义 {#customization}

### 额外字体 {#additional-fonts}

如果你想从另一个来源加载（额外的）字体或覆盖系统字体，你可以使用 [附加样式表] 添加相应的 `@font-face` 定义：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    @font-face {
      font-family: "<font>";
      src: "...";
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

然后，可以将字体应用到特定元素，例如仅限标题，或全局使用，作为站点范围的常规或等宽字体：

=== "常规字体"

    ``` css
    :root {
      --md-text-font: "<font>"; /* (1)! */
    }
    ```

    1.  始终通过 CSS 变量而不是 `font-family` 定义字体，因为这将禁用系统字体回退。

=== "等宽字体"

    ``` css
    :root {
      --md-code-font: "<font>";
    }
    ```

  [附加样式表]: ../customization.md#additional-css
