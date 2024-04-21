# 更改语言 {#changing-the-language}

Material for MkDocs 支持国际化 (i18n)，并提供 60 多种语言的模板变量和标签翻译。此外，网站
搜索可以配置为使用特定语言的词干分析器（如果可用的话）。

## 配置 {#configuration}

### 站点语言 {#site-language}

<!-- md:version 1.12.0 -->
<!-- md:default `en` -->

您可以在 `mkdocs.yml` 中设置站点语言：

``` yaml
theme:
  language: en # (1)!
```

1.  HTML5 仅允许为每个文档设置[单一语言]，这就是为什么 Material for MkDocs 只支持为整个项目设置一个规范语言，即每个 `mkdocs.yml` 一个。

    构建多语言文档的最简单方法是为每种语言创建一个子文件夹中的项目，然后使用[语言选择器]来互联这些项目。

以下语言得到支持：

<!-- hooks/translations.py -->

注意，由于默认 slug 函数的工作方式，某些语言会产生无法阅读的锚链接。考虑使用[支持 Unicode 的 slug 函数]。

!!! tip "缺少翻译？帮帮我们，只需 5 分钟"

    Material for MkDocs 依靠外部贡献来添加和更新它支持的 60 多种语言的翻译。如果您的语言显示某些翻译缺失，请点击链接添加它们。如果您的语言不在列表中，请点击这里[添加新语言]。

  [单一语言]: https://www.w3.org/International/questions/qa-html-language-declarations.en#attributes
  [语言选择器]: #site-language-selector
  [支持 Unicode 的 slug 函数]: extensions/python-markdown.md#toc-slugify
  [添加新语言]: https://github.com/squidfunk/mkdocs-material/issues/new?template=04-add-a-translation.yml&title=Add+translations+for+...

### 站点语言选择器 {#site-language-selector}

<!-- md:version 7.0.0 -->
<!-- md:default none -->

如果您的文档有多种语言版本，可以在页眉中添加一个指向这些语言的语言选择器。通过 `mkdocs.yml` 定义替代语言。

``` yaml
extra:
  alternate:
    - name: English
      link: /en/ # (1)!
      lang: en
    - name: Deutsch
      link: /de/
      lang: de
```

1.  注意这必须是一个绝对链接。如果它包含一个域部分，则按定义使用。否则，将[`site_url`][site_url]中设置的域部分添加到链接前。

每种替代语言有以下属性可用：

<!-- md:option alternate.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在语言选择器内用作语言名称，必须设置为非空字符串。

<!-- md:option alternate.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须设置为绝对链接，也可能指向另一个域或子域，不一定是用 MkDocs 生成的。

<!-- md:option alternate.lang -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须包含 [ISO 639-1 语言代码]，用于链接的 `hreflang` 属性，通过搜索引擎提高可发现性。

[![Language selector preview]][Language selector preview]

  [site_url]: https://www.mkdocs.org/user-guide/configuration/#site_url
  [ISO 639-1 language code]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
  [Language selector preview]: ../assets/screenshots/language-selection.png

#### 保持在页面上 {#stay-on-page}

<!-- md:sponsors -->
<!-- md:version insiders-4.47.0 -->
<!-- md:flag experimental -->

[Insiders] 提升了切换语言时的用户体验，例如，如果语言 `en` 和 `de` 包含具有相同路径名的页面，用户将留在当前页面：

=== "Insiders"

    ```
    docs.example.com/en/     -> docs.example.com/de/
    docs.example.com/en/foo/ -> docs.example.com/de/foo/
    docs.example.com/en/bar/ -> docs.example.com/de/bar/
    ```

=== "Material for MkDocs"

    ```
    docs.example.com/en/     -> docs.example.com/de/
    docs.example.com/en/foo/ -> docs.example.com/de/
    docs.example.com/en/bar/ -> docs.example.com/de/
    ```

无需配置。我们正在努力改进 2024 年的多语言支持，包括在未来使语言切换更加无缝。

  [Insiders]: ../insiders/index.md

### 文本方向 {#directionality}

<!-- md:version 2.5.0 -->
<!-- md:default computed -->

虽然许多语言是 `ltr`（从左到右阅读），Material for MkDocs 也支持 `rtl`（从右到左阅读）方向性，这是根据选择的语言推断出来的，但也可以设置为：

``` yaml
theme:
  direction: ltr
```

点击一个图块来改变文本方向：

<div class="mdx-switch">
  <button data-md-dir="ltr"><code>ltr</code></button>
  <button data-md-dir="rtl"><code>rtl</code></button>
</div>

<script>
  var buttons = document.querySelectorAll("button[data-md-dir]")
  buttons.forEach(function(button) {
    button.addEventListener("click", function() {
      var attr = this.getAttribute("data-md-dir")
      document.body.dir = attr
      var name = document.querySelector("#__code_2 code span.l")
      name.textContent = attr
    })
  })
</script>

## 自定义 {#customization}

### 自定义翻译 {#custom-translations}

如果您想自定义某种语言的一些翻译，请按照[主题扩展]指南操作，并在 `overrides` 文件夹中创建一个新的部分。然后，导入该语言的[翻译]作为后备，只需覆盖您想要修改的那些：

=== ":octicons-file-code-16: `overrides/partials/languages/custom.html`"

    ``` html
    <!-- Import translations for language and fallback -->
    {% import "partials/languages/de.html" as language %}
    {% import "partials/languages/en.html" as fallback %} <!-- (1)! -->

    <!-- Define custom translations -->
    {% macro override(key) %}{{ {
      "source.file.date.created": "Erstellt am", <!-- (2)! -->
      "source.file.date.updated": "Aktualisiert am"
    }[key] }}{% endmacro %}

    <!-- Re-export translations -->
    {% macro t(key) %}{{
      override(key) or language.t(key) or fallback.t(key)
    }}{% endmacro %}
    ```

    1.  注意 `en` 必须始终用作后备语言，因为它是默认的主题语言。

    2.  查看[可用语言列表]，选择您想为您的语言覆盖的翻译并添加它们。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    theme:
      language: custom
    ```

  [主题扩展]: ../customization.md#extending-the-theme
  [翻译]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/
  [可用语言列表]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/partials/languages/
