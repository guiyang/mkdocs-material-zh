---
icon: material/emoticon-happy-outline
---

# 图标与表情符号 Icons, Emojis {#icons-emojis}

Material for MkDocs 的最佳功能之一是可以在您的项目文档中使用[超过10,000个图标][图标搜索]和数千个表情符号，几乎不需要额外的努力。此外，还可以添加和使用[自定义图标]。

  [图标搜索]: #search
  [自定义图标]: ../setup/changing-the-logo-and-icons.md#additional-icons

## 搜索 {#search}

<div class="mdx-iconsearch" data-mdx-component="iconsearch">
  <input
    class="md-input md-input--stretch mdx-iconsearch__input"
    placeholder="Search the icon and emoji database"
    data-mdx-component="iconsearch-query"
  />
  <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result">
    <div class="mdx-iconsearch-result__meta"></div>
    <ol class="mdx-iconsearch-result__list"></ol>
  </div>
</div>
<small>
  :octicons-light-bulb-16:
  **Tip:** Enter some keywords to find icons and emojis and click on the
  shortcode to copy it to your clipboard.
</small>

## 配置 {#configuration}

此配置通过使用简单的短代码启用图标和表情符号的使用，这些短代码可以通过[图标搜索]找到。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
```

Material for MkDocs 预装了以下图标集：

- :material-material-design: – [Material Design]
- :fontawesome-brands-font-awesome: – [FontAwesome]
- :octicons-mark-github-16: – [Octicons]
- :simple-simpleicons: – [Simple Icons]

查看其他配置选项：

- [属性列表]
- [表情]
- [自定义图标的表情]

  [Material Design]: https://materialdesignicons.com/
  [FontAwesome]: https://fontawesome.com/search?m=free
  [Octicons]: https://octicons.github.com/
  [Simple Icons]: https://simpleicons.org/
  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [表情]: ../setup/extensions/python-markdown-extensions.md#emoji
  [自定义图标的表情]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.emoji.options.custom_icons

## 使用方法 {#usage]}

### 使用表情符号 {#using-emojis}

通过将表情符号的短代码放在两个冒号之间，可以在 Markdown 中集成表情符号。如果您使用 [Twemoji]（推荐），可以在 [Emojipedia] 查找短代码：

``` title="Emoji"
:smile:
```

<div class="result" markdown>

:smile:

</div>
  [Twemoji]: https://github.com/twitter/twemoji
  [Emojipedia]: https://emojipedia.org/twitter/


### 使用图标 {#using-icons}

启用 [表情] 后，可以通过引用主题中预装的图标的有效路径来类似地使用图标，这些图标位于 [`.icons`][自定义图标] 目录中，并将 `/` 替换为 `-`：

``` title="Icon"
:fontawesome-regular-face-laugh-wink:
```

<div class="result" markdown>

:fontawesome-regular-face-laugh-wink:

</div>

  [自定义图标]: https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons

#### 带颜色的 {#with-colors}

启用 [属性列表] 后，可以通过在图标后附加特殊语法添加自定义 CSS 类。虽然 HTML 允许使用[内联样式]，但总是推荐添加[额外样式表]并将声明移到专用的 CSS 类中：

<style>
  .youtube {
    color: #EE0F0F;
  }
</style>

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    .youtube {
      color: #EE0F0F;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

应用自定义后，将 CSS 类添加到图标短代码中：

``` markdown title="Icon with color"
:fontawesome-brands-youtube:{ .youtube }
```

<div class="result" markdown>

:fontawesome-brands-youtube:{ .youtube }

</div>

  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [内联样式]: https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/style
  [额外样式表]: ../customization.md#additional-css

#### 带动画的 {#with-animations}

类似于添加[颜色]，通过使用[额外样式表]定义一个 `@keyframes` 规则并向图标添加专用 CSS 类，也很容易为图标添加[动画]：

=== ":octicons-file-code-16: `docs/stylesheets/extra.css`"

    ``` css
    @keyframes heart {
      0%, 40%, 80%, 100% {
        transform: scale(1);
      }
      20%, 60% {
        transform: scale(1.15);
      }
    }
    .heart {
      animation: heart 1000ms infinite;
    }
    ```

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_css:
      - stylesheets/extra.css
    ```

应用自定义后，将 CSS 类添加到图标短代码中：

``` markdown title="Icon with animation"
:octicons-heart-fill-24:{ .heart }
```

<div class="result" markdown>

:octicons-heart-fill-24:{ .mdx-heart }

</div>

  [颜色]: #with-colors
  [动画]: https://developer.mozilla.org/en-US/docs/Web/CSS/animation

### 在侧边栏中使用图标和表情符号 :smile: {#icons-emojis-in-sidebars}

借助[内置排版插件]，您可以在标题中使用图标和表情符号，这些标题随后将在侧边栏中渲染。该插件保留 Markdown 和 HTML 格式。

  [内置排版插件]: ../plugins/typeset.md

## 自定义 {#customization}

### 在模板中使用图标 {#using-icons-in-templates}

当您[扩展主题]时，可以简单地引用任何[与主题捆绑的图标][图标搜索]，使用 Jinja 的[`include`][include]函数，并将其包裹在 `.twemoji` CSS 类中：

``` html
<span class="twemoji">
  {% include ".icons/fontawesome/brands/youtube.svg" %} <!-- (1)! -->
</span>
```

1.  Enter a few keywords to find the perfect icon using our [icon search] and
    click on the shortcode to copy it to your clipboard:

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="brands youtube" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

这正是 Material for MkDocs 在其模板中所做的。

  [扩展主题]: ../customization.md#extending-the-theme
  [include]: https://jinja.palletsprojects.com/en/2.11.x/templates/#include
