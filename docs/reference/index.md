# 参考 {#reference}

Material for MkDocs 配备了许多出色的功能，使技术写作成为一种愉快的活动。本文档部分解释了如何设置页面，并展示了可以直接从 Markdown 文件中使用的所有可用样本。

## 配置 {#configuration}

## 使用 {#usage}

### 设置页面 `title` {#setting-the-page-title}

每个页面都有一个指定的标题，用于导航侧边栏、[社交卡片]和其他地方。虽然 MkDocs 会尝试通过[四步过程]自动确定页面的标题，但也可以通过前置事项 `title` 属性显式设置标题：

``` yaml
---
title: Lorem ipsum dolor sit amet # (1)!
---

# Page title
...
```

1.  此行将生成页面的 HTML 文档的[`head`][head]中的[`title`][title]设置为给定值。请注意，通过[`site_name`][site_name]设置的站点标题会以破折号追加。

  [社交卡片]: ../setup/setting-up-social-cards.md
  [四步过程]: https://www.mkdocs.org/user-guide/writing-your-docs/#meta-data
  [title]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title
  [head]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head
  [site_name]: https://www.mkdocs.org/user-guide/configuration/#site_name

### 设置页面 `description` {#setting-the-page-description}

Markdown 文件可以包含添加到页面 `meta` 标签中的描述，并且也用于[社交卡片]。如果作者没有为 Markdown 文件明确定义描述，建议在 `mkdocs.yml` 中设置一个[`site_description`][site_description]作为后备值：

``` yaml
---
description: Nullam urna elit, malesuada eget finibus ut, ac tortor. # (1)!
---

# Page title
...
```

1.  此行在当前页面的文档 `head` 中设置包含描述的 `meta` 标签。

  [site_description]: https://www.mkdocs.org/user-guide/configuration/#site_description

### 设置页面 `icon` {#setting-the-page-icon}

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->

可以为每个页面分配一个图标，然后在导航侧边栏中以及启用时的[导航标签页]中渲染。使用前置事项 `icon` 属性引用一个图标，将以下行添加到 Markdown 文件顶部：

``` yaml
---
icon: material/emoticon-happy # (1)!
---

# Page title
...
```

1.  输入几个关键词在我们的[图标搜索]中找到完美的图标，并点击短码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="emoticon happy" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

  [Insiders]: ../insiders/index.md
  [图标搜索]: icons-emojis.md#search
  [导航标签页]: ../setup/setting-up-navigation.md#navigation-tabs

### 设置页面 `status` {#setting-the-page-status}

<!-- md:version 9.2.0 -->
<!-- md:flag experimental -->
<!-- md:example page-status -->

可以为每个页面分配一个状态，然后在导航侧边栏中显示。首先，通过在 `mkdocs.yml` 中添加以下内容，将状态标识符与描述关联起来：

``` yaml
extra:
  status:
    <identifier>: <description> # (1)!
```

1.  标识符只能包含字母数字字符、破折号和下划线。例如，如果您有一个状态 `Recently added`，您可以设置 `new` 作为标识符：

    ``` yaml
    extra:
      status:
        new: Recently added
    ```

现在可以使用前置事项 `status` 属性设置页面状态。例如，您可以用以下行将页面标记为 `new`：

``` yaml
---
status: new
---

# Page title
...
```

已经定义了以下状态标识符：

- :material-alert-decagram: – `new`
- :material-trash-can: – `deprecated`

您可以这样定义自定义页面状态，但如果您希望它有一个默认图标之外的图标，您还需要在您的 `extra.css` 中配置它。我们有一个[自定义页面状态的示例]可以帮助您入门。

[自定义页面状态的示例]: https://mkdocs-material.github.io/examples/page-status/

### 设置页面 `subtitle` {#setting-the-page-subtitle}

<!-- md:sponsors -->
<!-- md:version insiders-4.25.0 -->
<!-- md:flag experimental -->

每个页面都可以定义一个副标题，然后作为导航侧边栏的一部分渲染，方法是使用前置事项 `subtitle` 属性，并添加以下行：

``` yaml
---
subtitle: Nullam urna elit, malesuada eget finibus ut, ac tortor
---

# Page title
...
```

### 设置页面 `template` {#setting-the-page-template}

如果您正在使用[主题扩展]并在 `overrides` 目录中创建了一个新的页面模板，您可以为特定页面启用它。在 Markdown 文件顶部添加以下行：

``` yaml
---
template: custom.html
---

# Page title
...
```

??? question "如何为整个文件夹设置页面模板？"

    借助[内置 meta 插件]，您可以为整个部分及其嵌套页面设置自定义模板，方法是在相应文件夹中创建一个 `.meta.yml` 文件，内容如下：

    ``` yaml
    template: custom.html
    ```

  [主题扩展]: ../customization.md#extending-the-theme
  [内置 meta 插件]: ../plugins/meta.md

## 自定义 {#customization}

### 在模板中使用元数据 {#using-metadata-in-templates}

#### :material-check-all: 在所有页面上 {#on-all-pages}

为了在文档中添加自定义 `meta` 标签，您可以[扩展主题][主题扩展]并[覆盖 `extrahead` 块][overriding blocks]，例如通过 `robots` 属性为搜索引擎添加索引策略：

``` html
{% extends "base.html" %}

{% block extrahead %}
  <meta name="robots" content="noindex, nofollow" />
{% endblock %}
```

  [overriding blocks]: ../customization.md#overriding-blocks

#### :material-check: 在单个页面上 {#on-a-single-page}

如果您想在单个页面上设置 `meta` 标签，或者想为不同页面设置不同的值，您可以在模板覆盖中使用 `page.meta` 对象，例如：

``` html
{% extends "base.html" %}

{% block extrahead %}
  {% if page and page.meta and page.meta.robots %}
    <meta name="robots" content="{{ page.meta.robots }}" />
  {% else %}
    <meta name="robots" content="index, follow" />
  {% endif %}
{% endblock %}
```

现在，您可以像使用[`title`][title]和[`description`][description]那样使用 `robots` 设置值。注意，在这种情况下，模板定义了一个 `else` 分支，如果没有给定值，就会设置一个默认值。

  [title]: #setting-the-page-title
  [description]: #setting-the-page-description
