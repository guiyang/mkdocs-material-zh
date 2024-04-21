---
title: 内置博客插件
icon: material/newspaper-variant-outline
---

# 内置博客插件 {#built-in-blog-plugin}

博客插件使构建博客变得非常简单，无论是作为文档的辅助工具还是主要内容。专注于您的内容，而插件完成所有繁重的工作，生成所有最新文章的视图、[归档]和[分类]页面，可配置的[分页]等等。

  [归档]: #archive
  [分类]: #categories
  [分页]: #pagination

## 目标 {#objective}

### 工作原理 {#how-it-works}

插件扫描配置的[`posts`目录][config.post_dir]中的`.md`文件，自动生成分页视图[^1]。如果没有另外配置，插件会假设您的项目具有以下目录布局，并为您创建任何缺失的目录或文件：

  [^1]:
    视图是自动生成的页面，即，您的博客入口列出所有最新文章，以及列出通过[元数据]按时间顺序关联的所有文章的[归档]和[分类]页面。

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     └─ index.md
└─ mkdocs.yml
```

在[`blog`目录][config.blog_dir]中的`index.md`文件是进入您博客的入口 -- 一个分页视图，列出所有文章按时间逆序排列。此外，插件支持自动创建[归档]和[分类]页面，这些页面列出了一段时间内或某个分类的部分文章。

[文章URL][config.post_url_format]是完全可配置的，无论您是否希望URL包含文章的日期。渲染的日期总是显示在项目的[网站语言]的区域设置中。像在其他静态博客框架中一样，文章可以注明各种[元数据]，便于与其他[内置插件]（例如，[社交]和[标签]插件）轻松集成。

文章可以在嵌套文件夹中组织，具有适合您特定需求的目录布局，并且可以使用Material for MkDocs提供的所有组件和语法，包括[警告框]、[注释]、[代码块]、[内容选项卡]、[图表]、[图标]、[数学表达式]等。

  [元数据]: #metadata
  [内置插件]: index.md
  [社交]: social.md
  [标签]: tags.md
  [警告框]: ../reference/admonitions.md
  [注释]: ../reference/annotations.md
  [代码块]: ../reference/code-blocks.md
  [内容选项卡]: ../reference/content-tabs.md
  [图表]: ../reference/diagrams.md
  [图标]: ../reference/icons-emojis.md
  [数学表达式]: ../reference/math.md

### 何时使用 {#when-to-use-it}

如果您想在您的项目中添加一个博客，或因其出色的技术写作能力而从其他博客框架迁移到Material for MkDocs，这个插件是一个极好的选择，因为它可以完美地与许多其他内置插件集成：

<div class="grid cards" markdown>

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件使得将[元数据]应用到一部分文章变得简单，包括作者、标签、分类、草稿状态以及社交卡片布局。

    ---

    __简化文章元数据的组织、分类和管理__

-   :material-share-circle: &nbsp; __[内置社交插件][social]__

    ---

    社交插件自动为每个文章和页面生成美观且可定制的社交卡片，作为社交媒体上的预览显示。

    ---

    __当在社交媒体上分享您的博客链接时，会渲染美观的社交卡片__

-   :material-rabbit: &nbsp; __[内置优化插件][optimize]__

    ---

    优化插件自动识别并优化您项目中引用的所有媒体文件，使用压缩和转换技术。

    ---

    __您的博客加载更快，因为向您的用户提供了更小的图片__

-   :material-tag-text: &nbsp; __[Built-in tags plugin][tags]__

    ---

    标签插件允许将文章与项目中的页面分类，以提高它们的可发现性并将文章连接到您的文档。

    ---

    __您文档的标签系统与您的博客集成__

</div>

  [meta]: meta.md
  [social]: social.md
  [optimize]: optimize.md
  [tags]: tags.md

## 配置 {#configuration}

<!-- md:version 9.2.0 -->
<!-- md:plugin [blog] – built-in -->
<!-- md:flag multiple -->
<!-- md:flag experimental -->

与所有[内置插件]一样，开始使用博客插件很简单。只需在`mkdocs.yml`中添加以下几行，您就可以开始撰写您的第一篇文章了：

``` yaml
plugins:
  - blog
```

博客插件内置于Material for MkDocs中，无需安装。

  [blog]: blog.md
  [内置插件]: index.md

### 导航 {#navigation}

如果您在`mkdocs.yml`中没有配置站点导航，则无需做更多设置。博客[归档]和[分类]页面将自动出现在自动生成的导航下。

如果您定义了导航结构，则需要指定博客应该出现在哪里。为博客创建一个[带有索引页面的导航部分]：

```yaml
theme:
  name: material
  features:
    - navigation.indexes
nav:
  - ...
  - Blog:
    - blog/index.md
```

[归档]和[分类]页面将作为子部分出现在博客部分的页面下。在这种情况下，它们会出现在`index.md`之后。`index.md`文件的路径必须与[blog_dir][config.blog_dir]匹配。这意味着您可以随意命名博客导航项，如'博客'、'新闻'或'提示'。

[带有索引页面的导航部分]: ../setup/setting-up-navigation.md#section-index-pages

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用插件[构建您的项目]。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - blog:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

---

#### <!-- md:setting config.blog_dir -->

<!-- md:version 9.2.0 -->
<!-- md:default `blog` -->

使用此设置更改博客位于[`docs`目录][mkdocs.docs_dir]中的路径。生成的URL将包含此路径作为所有文章和视图的前缀。您可以更改它，方法如下：

=== "文档 + 博客"

    ``` yaml
    plugins:
      - blog:
          blog_dir: blog
    ```

=== "仅博客"

    ``` yaml
    plugins:
      - blog:
          blog_dir: .
    ```

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

---

#### <!-- md:setting config.blog_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

如果您的文章摘要相对较长，您可以使用此设置利用目录来显示文章标题。如果您想启用它，请使用：

``` yaml
plugins:
  - blog:
      blog_toc: true
```

### 文章 {#posts}

以下设置适用于文章：

---

#### <!-- md:setting config.post_dir -->

<!-- md:version 9.2.0 -->
<!-- md:default `{blog}/posts` -->

使用此设置更改存放文章的文件夹。通常不需要更改此设置，但如果您想重命名文件夹或更改其文件系统位置，请使用：

``` yaml
plugins:
  - blog:
      post_dir: "{blog}/articles"
```

请注意，[`posts`目录][config.post_dir]仅用于文章组织 - 它不包括在文章URL中，因为它们是由该插件自动生成的。

以下占位符可用：

- `blog` – [`blog` directory][config.blog_dir]

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

---

#### <!-- md:setting config.post_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `long` -->

使用此设置更改文章的日期格式。此插件使用[babel]根据配置的[网站语言]渲染日期。您可以使用[babel]的[模式语法]或以下简码：

=== "Monday, January 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: full
    ```

=== "January 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: long
    ```

=== "Jan 31, 2024"

    ``` yaml
    plugins:
      - blog:
          post_date_format: medium
    ```

=== "1/31/24"

    ``` yaml
    plugins:
      - blog:
          post_date_format: short
    ```

请注意，根据[网站语言]，其他语言的结果可能看起来不同。

  [babel]: https://pypi.org/project/Babel/
  [网站语言]: ../setup/changing-the-language.md#site-language
  [模式语法]: https://babel.pocoo.org/en/latest/dates.html#pattern-syntax

---

#### <!-- md:setting config.post_url_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy/MM/dd` -->

使用此设置更改文章URL中使用的日期格式。格式字符串必须遵循[babel]的[模式语法]，且不得包含空白。一些流行的选择：

=== ":material-link: blog/2024/01/31/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy/MM/dd
    ```

=== ":material-link: blog/2024/01/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy/MM
    ```

=== ":material-link: blog/2024/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_date_format: yyyy
    ```

如果您想从文章URL中删除日期，例如，当您的博客主要是常青内容时，您可以从[`post_url_format`][config.post_url_format]格式字符串中移除`date`占位符。

---

#### <!-- md:setting config.post_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `{date}/{slug}` -->

使用此设置更改生成文章URL时使用的格式字符串。您可以自由组合占位符，并使用斜杠或其他字符连接它们：

=== ":material-link: blog/2024/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_format: "{date}/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          post_url_format: "{slug}"
    ```

以下占位符可用：

- `categories` – 文章分类，通过[`categories_slugify`][config.categories_slugify]转换为slug
- `date` – 文章日期，使用[`post_url_date_format`][config.post_url_date_format]格式化
- `slug` – 文章标题，通过[`post_slugify`][config.post_slugify]转换为slug，或通过[`slug`][meta.slug]元数据属性显式设置
- `file` – 文章文件名，不包括`.md`文件扩展名

如果您删除了`date`占位符，请确保文章URL不会与托管在[`blog`目录][config.blog_dir]下的其他页面的URL发生冲突，因为这会导致未定义的行为。

---

#### <!-- md:setting config.post_url_max_categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `1` -->

如果[`post_url_format`][config.post_url_format]中包含`categories`占位符并且文章定义了分类，使用此设置设置文章URL中包含的分类数量上限：

``` yaml
plugins:
  - blog:
      post_url_format: "{categories}/{slug}"
      post_url_max_categories: 2
```

如果给定多个分类，则在slug化后用`/`连接。

---

#### <!-- md:setting config.post_slugify -->

<!-- md:version 9.2.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改从文章标题生成URL兼容slug的函数。默认情况下，使用[Python Markdown Extensions]中的[`slugify`][pymdownx.slugs.slugify]函数，如下所示：

``` yaml
plugins:
  - blog:
      post_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置对所有语言都是Unicode-aware，应该能为所有语言生成良好的slug。当然，您也可以提供自定义的slug化函数以获得更精细的控制。

  [pymdownx.slugs.slugify]: https://github.com/facelessuser/pymdown-extensions/blob/01c91ce79c91304c22b4e3d7a9261accc931d707/pymdownx/slugs.py#L59-L65
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/extras/slugs/

---

#### <!-- md:setting config.post_slugify_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default `-` -->

使用此设置更改传递给[`post_slugify`][config.post_slugify]中设置的slug化函数的分隔符。虽然默认是连字符，但可以设置为任何字符串，例如`_`：

``` yaml
plugins:
  - blog:
      post_slugify_separator: _
```

---

#### <!-- md:setting config.post_excerpt -->

<!-- md:version 9.2.0 -->
<!-- md:default `optional` -->

默认情况下，插件使文章摘要成为可选的。当文章未定义摘要时，视图包括整个文章。此设置可用于使文章摘要成为必需：

=== "可选"

    ``` yaml
    plugins:
      - blog:
          post_excerpt: optional
    ```

=== "必需"

    ``` yaml
    plugins:
      - blog:
          post_excerpt: required
    ```

当文章摘要为必需时，未定义摘要分隔符的文章会引发错误。因此，当您想确保所有文章都已定义摘要时，此设置很有用。

---

#### <!-- md:setting config.post_excerpt_max_authors -->

<!-- md:version 9.2.0 -->
<!-- md:default `1` -->

使用此设置设置文章摘要中呈现的作者数量上限。虽然每篇文章可能由多个作者撰写，但此设置允许限制显示的作者数量，甚至只显示一个作者，或在文章摘要中禁用作者：

=== "呈现最多2名作者"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_authors: 2
    ```

=== "禁用作者s"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_authors: 0
    ```

这仅适用于视图中的文章摘要。文章总是呈现所有作者。

---

#### <!-- md:setting config.post_excerpt_max_categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `5` -->

使用此设置设置文章摘要中呈现的分类数量上限。虽然每篇文章可能被分配到多个分类，但此设置允许限制显示的分类数量，甚至只显示一个分类，或在文章摘要中禁用分类：

=== "呈现最多2个分类"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_categories: 2
    ```

=== "禁用分类"

    ``` yaml
    plugins:
      - blog:
          post_excerpt_max_categories: 0
    ```

这仅适用于视图中的文章摘要。文章总是呈现所有分类。

---

#### <!-- md:setting config.post_excerpt_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default <code>&lt;!-- more --&gt;</code> -->

使用此设置设置插件在生成文章摘要时将寻找的分隔符。分隔符 __之前__ 的所有内容被认为是摘要的一部分：

``` yaml
plugins:
  - blog:
      post_excerpt_separator: <!-- more -->
```

通常使用HTML注释作为分隔符。

---

#### <!-- md:setting config.post_readtime -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应自动计算文章的阅读时间，然后在文章摘要以及文章本身中呈现：

``` yaml
plugins:
  - blog:
      post_readtime: false
```

---

#### <!-- md:setting config.post_readtime_words_per_minute -->

<!-- md:version 9.2.0 -->
<!-- md:default `265` -->

使用此设置更改预期读者每分钟阅读的单词数量，以计算文章的阅读时间。如果您想进行微调，请使用：

``` yaml
plugins:
  - blog:
      post_readtime_words_per_minute: 300
```

每分钟阅读265个单词被视为成年人的[平均阅读时间]。

  [平均阅读时间]: https://help.medium.com/hc/en-us/articles/214991667-Read-time

### 归档 {#archive}

以下设置适用于归档页面：

---

#### <!-- md:setting config.archive -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用归档页面。归档页面按逆序显示特定时间间隔（例如，年、月等）的所有文章。如果您想禁用归档页面，请使用：

``` yaml
plugins:
  - blog:
      archive: false
```

---

#### <!-- md:setting config.archive_name -->

<!-- md:version 9.2.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到导航中的归档部分的标题。如果省略此设置，则从翻译中获取。如果您想更改它，请使用：

``` yaml
plugins:
  - blog:
      archive_name: Archive
```

---

#### <!-- md:setting config.archive_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy` -->

使用此设置更改归档页面标题中使用的日期格式。格式字符串必须符合[babel]的[模式语法]。一些流行的选择：

=== "2024"

    ``` yaml
    plugins:
      - blog:
          archive_date_format: yyyy
    ```

=== "January 2024"

    ``` yaml
    plugins:
      - blog:
          archive_date_format: MMMM yyyy
    ```

请注意，根据[网站语言]，其他语言的结果可能看起来不同。

---

#### <!-- md:setting config.archive_url_date_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `yyyy` -->

使用此设置更改归档页面URL中使用的日期格式。格式字符串必须符合[babel]的[模式语法]，且不得包含空格。一些流行的选择：

=== ":material-link: blog/archive/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_date_format: yyyy
    ```

=== ":material-link: blog/archive/2024/01/"

    ``` yaml
    plugins:
      - blog:
          archive_url_date_format: yyyy/MM
    ```

---

#### <!-- md:setting config.archive_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `archive/{date}` -->

使用此设置更改生成归档页面URL时使用的格式字符串。您可以自由组合占位符，并使用斜杠或其他字符连接它们：

=== ":material-link: blog/archive/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_format: "archive/{date}"
    ```

=== ":material-link: blog/2024/"

    ``` yaml
    plugins:
      - blog:
          archive_url_format: "{date}"
    ```

以下占位符可用：

- `date` – 归档日期，使用[`archive_url_date_format`][config.archive_url_date_format]格式化

---

#### <!-- md:setting config.archive_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用归档页面的分页。此设置的值继承自[`pagination`][config.pagination]，除非显式设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      archive_pagination: false
```

---

#### <!-- md:setting config.archive_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `10` -->

使用此设置更改每个归档页面呈现的文章数量。此设置的值继承自[`pagination_per_page`][config.pagination_per_page]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      archive_pagination_per_page: 5
```

---

#### <!-- md:setting config.archive_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置利用目录显示所有归档页面上的文章标题。此设置的值继承自[`blog_toc`][config.blog_toc]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      archive_toc: true
```

### Categories

以下设置适用于分类页面：

---

#### <!-- md:setting config.categories -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用分类页面。分类页面按时间逆序显示特定分类的所有文章。如果您想禁用分类页面，请使用：

``` yaml
plugins:
  - blog:
      categories: false
```

---

#### <!-- md:setting config.categories_name -->

<!-- md:version 9.2.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到导航中的分类部分的标题。如果省略此设置，则从翻译中获取。如果您想更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_name: Categories
```

---

#### <!-- md:setting config.categories_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `category/{slug}` -->

使用此设置更改生成分类页面URL时使用的格式字符串。您可以自由组合占位符，并使用斜杠或其他字符连接它们：

=== ":material-link: blog/category/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          categories_url_format: "category/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          categories_url_format: "{slug}"
    ```

以下占位符可用：

- `slug` – 分类，通过[`categories_slugify`][config.categories_slugify]转换为slug

---

#### <!-- md:setting config.categories_slugify -->

<!-- md:version 9.2.0 -->
<!-- md:default [`pymdownx.slugs.slugify`][pymdownx.slugs.slugify] -->

使用此设置更改从分类生成URL兼容slug的函数。默认情况下，使用[Python Markdown Extensions]中的[`slugify`][pymdownx.slugs.slugify]函数，如下所示：

``` yaml
plugins:
  - blog:
      categories_slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

默认配置对所有语言都是Unicode-aware，应该能为所有语言生成良好的slug。当然，您也可以提供自定义的slug化函数以获得更精细的控制。

---

#### <!-- md:setting config.categories_slugify_separator -->

<!-- md:version 9.2.0 -->
<!-- md:default `-` -->

使用此设置更改传递给[`categories_slugify`][config.categories_slugify]中设置的slug化函数的分隔符。虽然默认是连字符，但可以设置为任何字符串，例如`_`：

``` yaml
plugins:
  - blog:
      categories_slugify_separator: _
```

---

#### <!-- md:setting config.categories_sort_by -->

<!-- md:sponsors -->
<!-- md:version insiders-4.45.0 -->
<!-- md:default `material.plugins.blog.view_name` -->

使用此设置指定用于对分类进行排序的自定义函数。例如，如果您想按它们包含的文章数量对分类进行排序，请使用以下配置：

``` yaml
plugins:
  - blog:
      categories_sort_by: !!python/name:material.plugins.blog.view_post_count
```

不要忘记启用[`categories_sort_reverse`][config.categories_sort_reverse]。您可以定义自己的比较函数，该函数必须返回可在排序时进行比较的内容，即字符串或数字。

---

#### <!-- md:setting config.categories_sort_reverse -->

<!-- md:sponsors -->
<!-- md:version insiders-4.45.0 -->
<!-- md:default `false` -->

使用此设置反转分类排序的顺序。默认情况下，分类按升序排序，但您可以按以下方式反转排序：

``` yaml
plugins:
  - blog:
      categories_sort_reverse: true
```

---

#### <!-- md:setting config.categories_allowed -->

<!-- md:version 9.2.0 -->
<!-- md:default none -->

插件允许根据预定义列表检查分类，以捕捉拼写错误或确保不会随意添加分类。指定您要允许的分类：

``` yaml
plugins:
  - blog:
      categories_allowed:
        - Search
        - Performance
```

如果文章引用的分类不在此列表中，插件将停止构建。可以使用[`categories`][meta.categories]元数据属性将文章分配给分类。

---

#### <!-- md:setting config.categories_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用分类页面的分页。此设置的值继承自[`pagination`][config.pagination]，除非显式设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      categories_pagination: false
```

---

#### <!-- md:setting config.categories_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->
<!-- md:default `10` -->

使用此设置更改每个分类页面呈现的文章数量。此设置的值继承自[`pagination_per_page`][config.pagination_per_page]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_pagination_per_page: 5
```

---

#### <!-- md:setting config.categories_toc -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置利用目录显示所有分类页面上的文章标题。此设置的值继承自[`blog_toc`][config.blog_toc]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      categories_toc: true
```

### 作者

以下设置适用于作者：

---

#### <!-- md:setting config.authors -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用文章作者。如果启用此设置，插件将查找名为[`.authors.yml`][config.authors_file]的文件，并在文章和视图中渲染作者。禁用此行为：

``` yaml
plugins:
  - blog:
      authors: false
```

---

#### <!-- md:setting config.authors_file -->

<!-- md:version 9.2.0 -->
<!-- md:default `{blog}/.authors.yml` -->

使用此设置更改存储您文章的作者信息的文件的路径。通常不需要更改此设置，但如果您需要，请使用：

``` yaml
plugins:
  - blog:
      authors_file: "{blog}/.authors.yml"
```

以下占位符可用：

- `blog` – [`blog`目录][config.blog_dir]

提供的路径是从[`docs`目录][mkdocs.docs_dir]解析的。

!!! info "作者信息格式"

    `.authors.yml`文件必须遵循以下格式：

    ``` yaml title=".authors.yml"
    authors:
      <author>:
        name: string        # Author name
        description: string # Author description
        avatar: url         # Author avatar
        slug: url           # Author profile slug
        url: url            # Author website URL
    ```

    请注意，`<author>`必须设置为关联作者与文章的标识符，例如，GitHub用户名如`squidfunk`。然后可以在文章的[`authors`][meta.authors]元数据属性中使用此标识符。支持多个作者。例如，参见我们博客中使用的[`.authors.yml`文件][.authors.yml]。

  [.authors.yml]: https://github.com/squidfunk/mkdocs-material/blob/master/docs/blog/.authors.yml

---

#### <!-- md:setting config.authors_profiles -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `false` -->

使用此设置启用或禁用自动生成的作者档案。作者档案按时间逆序显示某一作者的所有文章。您可以启用作者档案：

``` yaml
plugins:
  - blog:
      authors_profiles: true
```

---

#### <!-- md:setting config.authors_profiles_name -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default computed -->

使用此设置更改插件添加到导航中的作者部分的标题。如果省略此设置，则从翻译中获取。如果您想更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_name: Authors
```

---

#### <!-- md:setting config.authors_profiles_url_format -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `author/{slug}` -->

使用此设置更改生成作者档案URL时使用的格式字符串。您可以自由组合占位符，并使用斜杠或其他字符连接它们：

=== ":material-link: blog/author/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          authors_profiles_url_format: "author/{slug}"
    ```

=== ":material-link: blog/:material-dots-horizontal:/"

    ``` yaml
    plugins:
      - blog:
          authors_profiles_url_format: "{slug}"
    ```

以下占位符可用：

- `slug` – 从[`authors_file`][config.authors_file]中的作者标识或slug
- `name` – 从[`authors_file`][config.authors_file]中的作者名字

---

#### <!-- md:setting config.authors_profiles_pagination -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用作者档案的分页。此设置的值继承自[`pagination`][config.pagination]，除非显式设置。要禁用分页，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_pagination: false
```

---

#### <!-- md:setting config.authors_profiles_pagination_per_page -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `10` -->

使用此设置更改每个作者档案页面呈现的文章数量。此设置的值继承自[`pagination_per_page`][config.pagination_per_page]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_pagination_per_page: 5
```

---

#### <!-- md:setting config.authors_profiles_toc -->

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:default `false` -->

使用此设置利用目录显示所有作者档案上的文章标题。此设置的值继承自[`blog_toc`][config.blog_toc]，除非显式设置。要更改它，请使用：

``` yaml
plugins:
  - blog:
      authors_profiles_toc: true
```

### 分页 {#pagination}

以下设置适用于分页：

---

#### <!-- md:setting config.pagination -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用视图中的分页 -- 生成显示文章或文章子集的页面，按时间逆序排列。如果您想禁用分页，请使用：

``` yaml
plugins:
  - blog:
      pagination: false
```

---

#### <!-- md:setting config.pagination_per_page -->

<!-- md:version 9.2.0 -->
<!-- md:default `10` -->

使用此设置更改每页呈现的文章数量。如果您的文章摘要比较长，减少每页的文章数量可能是一个好主意：

``` yaml
plugins:
  - blog:
      pagination_per_page: 5
```

---

#### <!-- md:setting config.pagination_url_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `page/{page}` -->

使用此设置更改生成分页视图URL时使用的格式字符串。您可以自由组合占位符，并使用斜杠或其他字符连接它们：

=== ":material-link: blog/page/n/"

    ``` yaml
    plugins:
      - blog:
          pagination_url_format: "page/{page}"
    ```

=== ":material-link: blog/n/"

    ``` yaml
    plugins:
      - blog:
          pagination_url_format: "{page}"
    ```

以下占位符可用：

- `page` – 页码

---

#### <!-- md:setting config.pagination_format -->

<!-- md:version 9.2.0 -->
<!-- md:default `~2~` -->

插件使用[paginate]模块使用特殊语法生成分页标记。使用此设置自定义分页的构建方式。一些流行的选择：

=== "1 2 3 .. n"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "~2~"
    ```

=== "1 2 3 .. n :material-chevron-right: :material-chevron-double-right:"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "$link_first $link_previous ~2~ $link_next $link_last"
    ```

=== "1 :material-chevron-right:"

    ``` yaml
    plugins:
      - blog:
          pagination_format: "$link_previous $page $link_next"
    ```

[paginate]支持以下占位符：

- `#!css $first_page` – 第一个可达页面的编号
- `#!css $last_page` – 最后一个可达页面的编号
- `#!css $page` – 当前选定页面的编号
- `#!css $page_count` – 可达页面的数量
- `#!css $items_per_page` – 每页最大项目数量
- `#!css $first_item` – 当前页面上第一个项目的索引
- `#!css $last_item` – 当前页面上最后一个项目的索引
- `#!css $item_count` – 项目总数
- `#!css $link_first` – 链接到第一页（除非已在第一页）
- `#!css $link_last` – 链接到最后一页（除非已在最后一页）
- `#!css $link_previous` – 链接到上一页（除非已在第一页）
- `#!css $link_next` – 链接到下一页（除非已在最后一页）

  [paginate]: https://pypi.org/project/paginate/

---

#### <!-- md:setting config.pagination_if_single_page -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置控制是否在视图仅由单页组成时自动禁用分页。如果您想始终呈现分页，请使用：

``` yaml
plugins:
  - blog:
      pagination_if_single_page: true
```

---

#### <!-- md:setting config.pagination_keep_content -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

使用此设置启用或禁用内容持久化，即，分页视图是否也应显示其包含视图的内容。如果您想启用此行为，请使用：

``` yaml
plugins:
  - blog:
      pagination_keep_content: true
```

### 草稿 {#drafts}

以下设置适用于草稿：

---

#### <!-- md:setting config.draft -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

渲染[草稿文章][meta.draft]在部署预览中可能很有用。使用此设置指定插件是否应包括标记为草稿的文章，当[构建您的项目]时：

=== "渲染草稿"

    ``` yaml
    plugins:
      - blog:
          draft: true
    ```

=== "不渲染草稿"

    ``` yaml
    plugins:
      - blog:
          draft: false
    ```

---

#### <!-- md:setting config.draft_on_serve -->

<!-- md:version 9.2.0 -->
<!-- md:default `true` -->

使用此设置控制插件是否应包括标记为草稿的文章，当[预览您的网站]时。如果您不希望在预览时包括草稿文章，请使用：

``` yaml
plugins:
  - blog:
      draft_on_serve: false
```

  [预览您的网站]: ../creating-your-site.md#previewing-as-you-write

---

#### <!-- md:setting config.draft_if_future_date -->

<!-- md:version 9.2.0 -->
<!-- md:default `false` -->

插件可以自动将具有未来日期的文章标记为草稿。当日期超过今天时，除非明确标记为草稿，否则在[构建您的项目]时文章会自动被包括：

``` yaml
plugins:
  - blog:
      draft_if_future_date: true
```

## 使用方法 {#usage}

### 元数据 {#metadata}

文章可以定义一些元数据属性，这些属性指定插件如何渲染它们，它们如何集成到哪些视图中，以及它们如何相互链接。每篇文章的元数据都会根据一个模式进行验证，以便更快地发现语法错误。

以下属性可用：

---

#### <!-- md:setting meta.authors -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将文章与[作者]关联起来，通过提供在[`authors_file`][config.authors_file]中定义的标识符列表。如果无法解析作者，插件将终止并报错：

``` yaml
---
authors:
  - squidfunk # (1)!
---

# Post title
...
```

1.  通过使用它们的标识符链接作者。例如，参见我们博客中使用的[`.authors.yml` 文件][.authors.yml]。

  [作者]: #authors

---

#### <!-- md:setting meta.categories -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将文章与一个或多个[Categories][分类]关联起来，使文章成为生成的分类页面的一部分。分类定义为字符串列表（允许使用空格）：

``` yaml
---
categories:
  - Search
  - Performance
---

# Post title
...
```

如果您想防止意外的拼写错误将分类分配给文章，您可以在`mkdocs.yml`中使用[`categories_allowed`][config.categories_allowed]设置来设定允许的分类预定义列表。

---

#### <!-- md:setting meta.date -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:flag required -->

使用此属性指定文章的日期。请注意，此属性是必需的，这意味着如果未设置，构建将失败。可以使用稍微不同的语法设置额外的日期：

=== "日期"

    ``` yaml
    ---
    date: 2024-01-31
    ---

    # Post title
    ...
    ```

=== "更新日期"

    ``` yaml
    ---
    date:
      created: 2024-01-31 # (1)!
      updated: 2024-02-01
    ---

    # Post title
    ...
    ```

    1.  每篇文章都必须设置一个创建日期。

=== "自定义日期"

    ``` yaml
    ---
    date:
      created: 2024-01-31
      my_custom_date: 2024-02-01 # (1)!
    ---

    # Post title
    ...
    ```

    1.  博客插件验证所有日期，并允许使用[babel]的[模式语法]在模板中格式化它们。当使用主题扩展时，作者可以在模板中添加自定义日期。

        这最初是在#5733中请求的。

支持以下日期格式：

- `2024-01-31`
- `2024-01-31T12:00:00`

---

#### <!-- md:setting meta.draft -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性将文章标记为草稿。插件允许在[构建您的项目]时使用[`draft`][config.draft]设置包括或排除标记为草稿的文章。将文章标记为草稿：

``` yaml
---
draft: true
---

# Post title
...
```

---

#### <!-- md:setting meta.pin -->

<!-- md:sponsors -->
<!-- md:version insiders-4.53.0 -->
<!-- md:flag metadata -->
<!-- md:default `false` -->
<!-- md:flag experimental -->

使用此属性将文章固定在视图的顶部。如果有多篇文章被固定，这些固定的文章将按降序排序，并显示在所有其他文章之前。固定文章：

``` yaml
---
pin: true
---

# Post title
...
```

---

#### <!-- md:setting meta.links -->

<!-- md:sponsors -->
<!-- md:version insiders-4.23.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->
<!-- md:flag experimental -->

使用此属性定义在文章侧边栏中呈现的链接列表。该属性遵循与`mkdocs.yml`中的[`nav`][mkdocs.nav]相同的语法，支持部分和甚至锚点：

=== "链接"

    ``` yaml
    ---
    links:
      - setup/setting-up-site-search.md
      - insiders/index.md
    ---

    # Post title
    ...
    ```

=== "带部分的链接"

    ``` yaml
    ---
    links:
      - setup/setting-up-site-search.md
      - Insiders:
        - insiders/index.md
        - insiders/getting-started.md
    ---

    # Post title
    ...
    ```

=== "带锚点的链接"

    ``` yaml
    ---
    links:
      - plugins/search.md # (1)!
      - Insiders:
        - insiders/index.md#how-to-become-a-sponsor
        - insiders/getting-started.md#requirements
    ---

    # Post title
    ...
    ```

    1.  如果链接定义了一个锚点，插件将从链接的页面解析锚点，并将锚点标题设置为[副标题]。

所有相对链接都从[`docs`目录][mkdocs.docs_dir]解析。

  [副标题]: ../reference/index.md#setting-the-page-subtitle

---

#### <!-- md:setting meta.readtime -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default computed -->

使用此属性明确设置文章的阅读时间（以分钟为单位）。当启用[`post_readtime`][config.post_readtime]时，插件计算文章的阅读时间，这可以被覆盖：

``` yaml
---
readtime: 15
---

# Post title
...
```

---

#### <!-- md:setting meta.slug -->

<!-- md:version 9.2.0 -->
<!-- md:flag metadata -->
<!-- md:default computed -->

使用此属性明确设置文章的slug。默认情况下，文章的slug由[`post_slugify`][config.post_slugify]函数从文章标题自动计算，这可以被覆盖：

``` yaml
---
slug: help-im-trapped-in-a-universe-factory
---

# Post title
...
```

Slug被传递到[`post_url_format`][config.post_url_format]。

---

!!! question "有缺少的功能吗？"

    当您设置您的博客或从其他博客框架迁移时，您可能会发现缺少特定功能——我们很乐意考虑将其添加到插件中！您可以[开启讨论]询问问题，或在我们的[问题跟踪器]上创建[变更请求]，以便我们了解它是否适合该插件。

  [开启讨论]: https://github.com/squidfunk/mkdocs-material/discussions
  [变更请求]: ../contributing/requesting-a-change.md
  [问题跟踪器]: https://github.com/squidfunk/mkdocs-material/issues
