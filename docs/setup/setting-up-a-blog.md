# 设置博客 {#setting-up-a-blog}

Material for MkDocs 让建立博客变得非常简单，无论是作为您文档的辅助功能还是独立存在。专注于您的内容，而引擎则自动完成所有繁重的工作，自动生成[归档]和[分类]索引、[文章短链接]、可配置的[分页]等。

---

__Check out our [blog], which is created with the new [built-in blog plugin]!__

  [归档]: ../plugins/blog.md#archive
  [分类]: ../plugins/blog.md#categories
  [文章短链接]: ../plugins/blog.md#config.post_url_format
  [分页]: ../plugins/blog.md#pagination
  [blog]: ../blog/index.md

## 配置 {#configuration}

### 内置博客插件 {#built-in-blog-plugin}

<!-- md:version 9.2.0 -->
<!-- md:plugin -->
<!-- md:flag experimental -->

内置博客插件支持从一个包含带有日期和其他结构化数据的帖子的文件夹构建博客。首先，将以下行添加到 `mkdocs.yml` 中：

``` yaml
plugins:
  - blog
```

有关所有设置的列表，请查阅[插件文档]。

  [插件文档]: ../plugins/blog.md

#### 高级设置 {#advanced-settings}

<!-- md:sponsors -->
<!-- md:version insiders-4.44.0 -->

以下高级设置目前仅限于我们的[赞助者][Insiders]。它们完全是可选的，并不影响博客的功能，但可以帮助自定义：

- [`archive_pagination`][config.archive_pagination]
- [`archive_pagination_per_page`][config.archive_pagination_per_page]
- [`categories_sort_by`][config.categories_sort_by]
- [`categories_sort_reverse`][config.categories_sort_reverse]
- [`categories_pagination`][config.categories_pagination]
- [`categories_pagination_per_page`][config.categories_pagination_per_page]
- [`authors_profiles_pagination`][config.authors_profiles_pagination]
- [`authors_profiles_pagination_per_page`][config.authors_profiles_pagination_per_page]

我们会在这里添加更多设置，随着我们发现新的使用场景。

  [Insiders]: ../insiders/index.md
  [内置博客插件]: ../plugins/blog.md
  [built-in plugins]: ../insiders/getting-started.md#built-in-plugins
  [docs_dir]: https://www.mkdocs.org/user-guide/configuration/#docs_dir
  [start writing your first post]: #writing-your-first-post

  [config.archive_pagination]: ../plugins/blog.md#config.archive_pagination
  [config.archive_pagination_per_page]: ../plugins/blog.md#config.archive_pagination_per_page
  [config.categories_sort_by]: ../plugins/blog.md#config.categories_sort_by
  [config.categories_sort_reverse]: ../plugins/blog.md#config.categories_sort_reverse
  [config.categories_pagination]: ../plugins/blog.md#config.categories_pagination
  [config.categories_pagination_per_page]: ../plugins/blog.md#config.categories_pagination_per_page
  [config.authors_profiles_pagination]: ../plugins/blog.md#config.authors_profiles_pagination
  [config.authors_profiles_pagination_per_page]: ../plugins/blog.md#config.authors_profiles_pagination_per_page

### RSS

<!-- md:version 9.2.0 -->
<!-- md:plugin [rss] -->

[内置博客插件]与[RSS 插件][rss]无缝集成，后者提供了一种简单的方式来向您的博客（或整个文档）添加 RSS 源。使用 `pip` 安装它：

```
pip install mkdocs-rss-plugin
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - rss:
      match_path: blog/posts/.* # (1)!
      date_from_meta:
        as_creation: date
      categories:
        - categories
        - tags # (2)!
```

1.  RSS 插件允许筛选要包含在源中的 URL。在此示例中，只有博客帖子将包含在源中。

2.  如果您想在源中包括帖子的分类和标签，请在此处添加 `categories` 和 `tags`。

以下配置选项受支持：

<!-- md:option rss.enabled -->

:   <!-- md:default `true` --> 此选项指定构建项目时插件是否启用。如果您想加快本地构建速度，可以使用[环境变量]：

    ``` yaml
    plugins:
      - rss:
          enabled: !ENV [CI, false]
    ```

<!-- md:option rss.match_path -->

:   <!-- md:default `.*` --> 此选项指定应包括在源中的页面。例如，要仅包括博客帖子，请使用以下正则表达式：

    ``` yaml
    plugins:
      - rss:
          match_path: blog/posts/.*
    ```

<!-- md:option rss.date_from_meta -->

:   <!-- md:default none --> 此选项指定应用作源中页面的创建日期的前置元素属性。建议使用 `date` 属性：

    ``` yaml
    plugins:
      - rss:
          date_from_meta:
            as_creation: date
    ```

<!-- md:option rss.categories -->

:   <!-- md:default none --> 此选项指定用作源部分的分类的前置元素属性。如果您使用[分类]和[标签]，请使用以下行添加两者：

    ``` yaml
    plugins:
      - rss:
          categories:
            - categories
            - tags
    ```

<!-- md:option rss.comments_path -->

:   <!-- md:default none --> 此选项指定可找到帖子或页面评论的锚点。如果您集成了[评论系统]，请添加以下行：

    ``` yaml
    plugins:
      - rss:
          comments_path: "#__comments"
    ```

Material for MkDocs 将自动向您的网站添加[必要的元数据]，使浏览器和阅读器能够发现 RSS 源。请注意，[RSS 插件][rss] 还包含其他几个配置选项。有关详细信息，请参阅[文档]。

  [rss]: https://guts.github.io/mkdocs-rss-plugin/
  [categories]: ../plugins/blog.md#categories
  [标签]: setting-up-tags.md#built-in-tags-plugin
  [评论系统]: adding-a-comment-system.md
  [必要的元数据]: https://guts.github.io/mkdocs-rss-plugin/configuration/#integration
  [theme extension]: ../customization.md
  [文档]: https://guts.github.io/mkdocs-rss-plugin/configuration/

### 仅博客 {#blog-only}

您可能需要构建一个纯博客，没有任何文档。在这种情况下，您可以创建如下文件树：

``` { .sh .no-copy }
.
├─ docs/
│  ├─ posts/ # (1)!
│  ├─ .authors.yml
│  └─ index.md
└─ mkdocs.yml
```

1.  注意，`posts` 目录位于 `docs` 的根部，没有中间的 `blog` 目录。

并在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - blog:
      blog_dir: . # (1)!
```

1.  更多关于 [blog_dir](../plugins/blog.md#config.blog_dir) 的信息

有了这个配置，博客帖子的 URL 将是 `/<post_slug>`，而不是 `/blog/<post_slug>`。

## 使用 {#usage}

### 写你的第一篇帖子 {#writing-your-first-post}

在您成功设置[内置博客插件]后，是时候写下您的第一篇帖子了。该插件不假设任何特定的目录结构，因此您在组织帖子方面完全自由，只要它们都位于 `posts` 目录中：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     │  └─ hello-world.md # (1)!
│     └─ index.md
└─ mkdocs.yml
```

1.  如果您想以不同的方式安排帖子，您可以自由这样做。URL 是根据[`文章网址格式`][文章短链接]以及帖子的标题和日期构建的，无论它们在 `posts` 目录中如何组织。

创建一个名为 `hello-world.md` 的新文件，并添加以下行：

``` yaml
---
draft: true # (1)!
date: 2024-01-31 # (2)!
categories:
  - Hello
  - World
---

# Hello world!
...
```

1.  如果您将一篇帖子标记为[草稿]，则在索引页面的帖子日期旁边会出现红色标记。当网站构建时，草稿不会包含在输出中。[这种行为可以改变]，例如为构建部署预览时渲染草稿。

2.  如果您希望提供多个日期，可以使用以下语法，允许您定义上次更新博客帖子的日期 + 您可以添加到模板中的其他自定义日期：

    ``` yaml
    ---
    date:
      created: 2022-01-31
      updated: 2022-02-02
    ---

    # Hello world!
    ```

    请注意，创建日期 __必须__ 设置在 `date.created` 下，因为每篇博客帖子必须设置创建日期。

当您启动[实时预览服务]时，您应该会看到您的第一篇帖子！您还会意识到，[归档]和[分类]索引已为您自动生成。

  [草稿]: ../plugins/blog.md#drafts
  [这种行为可以改变]: ../plugins/blog.md#config.draft
  [实时预览服务]: ../creating-your-site.md#previewing-as-you-write

#### 添加摘要 {#adding-an-excerpt}

博客索引以及[归档]和[分类]索引可以列出每篇帖子的全部内容，或者帖子的摘要。通过在帖子的前几段后添加 `<!-- more -->` 分隔符，可以创建摘要：

``` py
# Hello world!

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
massa, nec semper lorem quam in massa.

<!-- more -->
...
```

当[内置博客插件]生成所有索引时，自动提取[摘要分隔符]前的内容，允许用户在决定跳进阅读前开始阅读帖子。

  [摘要分隔符]: ../plugins/blog.md#config.post_excerpt_separator

#### 添加作者 {#adding-authors}

为了为您的帖子添加更多个性，您可以将每篇帖子与一个或多个[作者]关联。首先，在您的博客目录中创建[`.authors.yml`][authors_file]文件，并添加一个作者：

``` yaml
authors:
  squidfunk:
    name: Martin Donath
    description: Creator
    avatar: https://github.com/squidfunk.png
```

[`.authors.yml`][authors_file] 文件将每个作者与一个标识符（在此示例中为 `squidfunk`）关联起来，然后可以在帖子中使用。可以配置不同的属性。有关所有可能属性的列表，请查阅[`authors_file`][authors_file]文档。

现在，您可以通过在 Markdown 文件的前置元素中引用其标识符，将一个或多个`作者`分配给一篇帖子。对于每位作者，每篇帖子的左侧边栏以及索引页面上的帖子摘要中都会渲染一个小型个人资料：

``` yaml
---
date: 2024-01-31
authors:
  - squidfunk
    ...
---

# Hello world!
...
```

  [作者]: ../plugins/blog.md#authors
  [authors_file]: ../plugins/blog.md#config.authors_file

#### 添加作者档案 {#adding-author-profiles}

<!-- md:sponsors -->
<!-- md:version insiders-4.46.0 -->
<!-- md:flag experimental -->

如果您希望为每位作者添加一个专 dedicated 页面，您可以通过将[`authors_profiles`][authors_profiles]配置选项设置为`true`来启用作者档案。只需将以下行添加到 `mkdocs.yml` 中：

``` yaml
plugins:
  - blog:
      authors_profiles: true
```

如果您将此与[自定义索引页面]结合使用，您可以为每位作者创建一个专属页面，包括简短描述、社交媒体链接等内容——基本上您可以用 Markdown 编写的任何内容。然后，帖子列表将附加在页面内容之后。

  [authors_profiles]: ../plugins/blog.md#config.authors_profiles
  [自定义索引页面]: #custom-index-pages

#### 添加分类 {#adding-categories}

分类是在专门的索引页面上按主题分组您的帖子的绝佳方式。这样，对特定主题感兴趣的用户可以探索您关于该主题的所有帖子。确保[分类]已启用并将其添加到前置元素 `categories` 属性中：

``` yaml
---
date: 2024-01-31
categories:
  - Hello
  - World
---

# Hello world!
...
```

如果您想避免在输入分类时打字错误，您可以在 `mkdocs.yml` 中定义您希望的分类，作为[`categories_allowed`][categories_allowed]配置选项的一部分。[内置博客插件]将在未在列表中找到分类时停止构建。

  [categories_allowed]: ../plugins/blog.md#config.categories_allowed

#### 添加标签 {#adding-tags}

除了[分类]，[内置博客插件]还与[内置标签插件]集成。如果您在帖子的前置元素 `tags` 属性中添加标签，则帖子将从[标签索引]中链接：

``` yaml
---
date: 2024-01-31
tags:
  - Foo
  - Bar
---

# Hello world!
...
```

像往常一样，标签渲染在主标题上方，并且帖子在标签索引页面上链接（如果配置）。请注意，帖子与页面一样，只能通过其标题链接。

  [内置标签插件]: ../plugins/tags.md
  [tags index]: setting-up-tags.md#adding-a-tags-index

#### 更改短链接 {#changing-the-slug}

短链接是用于 URL 中的帖子的缩写描述。它们是自动生成的，但您可以为页面指定自定义短链接：

``` yaml
---
slug: hello-world
---

# Hello there world!
...
```

#### 添加相关链接 {#adding-related-links}

<!-- md:sponsors -->
<!-- md:version insiders-4.23.0 -->
<!-- md:flag experimental -->

相关链接提供了一种完美的方式，在左侧边栏中突出显示帖子的 _进一步阅读_ 部分，引导用户前往您文档的其他目的地。使用前置元素 `links` 属性为帖子添加相关链接：

``` yaml
---
date: 2024-01-31
links:
  - plugins/search.md
  - insiders/index.md#how-to-become-a-sponsor
---

# Hello world!
...
```

您可以使用与`mkdocs.yml`中的[`nav`][nav]部分相同的语法，这意味着您可以为链接设置显式标题、添加外部链接甚至使用嵌套：

``` yaml
---
date: 2024-01-31
links:
  - plugins/search.md
  - insiders/index.md#how-to-become-a-sponsor
  - Nested section:
    - External link: https://example.com
    - setup/setting-up-site-search.md
---

# Hello world!
...
```

如果您仔细观察，您会意识到您甚至可以使用锚点链接到文档的特定部分，扩展[`nav`][nav]在`mkdocs.yml`中的语法的可能性。[内置博客插件]解析锚点并将锚点的标题设置为相关链接的[副标题]。

请注意，所有链接都必须相对于[`docs_dir`][docs_dir]，这也适用于[`nav`][nav]设置。

  [nav]: https://www.mkdocs.org/user-guide/configuration/#nav
  [副标题]: ../reference/index.md#setting-the-page-subtitle

#### 从帖子链接和到帖子链接 {#linking-from-and-to-posts}

虽然[帖子 URL][文章短链接]是动态计算的，[内置博客插件]确保所有从帖子和帖子资产到帖子的链接都是正确的。如果您想链接到一个帖子，只需使用 Markdown 文件的路径作为链接引用（链接必须是相对的）：

``` markdown
[Hello World!](blog/posts/hello-world.md)
```

从帖子链接到页面，例如索引，遵循相同的方法：
``` markdown
[Blog](../index.md)
```

`posts`目录中的所有资产都会在站点构建时复制到`blog/assets`文件夹中。当然，您也可以从`posts`目录外的帖子引用资产。[内置博客插件]确保所有链接都是正确的。

#### 固定帖子 :material-alert-decagram:{ .mdx-pulse title="2024年2月24日添加" } {#pinning-a-post}

<!-- md:sponsors -->
<!-- md:version insiders-4.53.0 -->
<!-- md:flag experimental -->

如果您想将一篇帖子固定在索引页面的顶部，以及它所属的归档和分类索引中，您可以使用前置元素 `pin` 属性：

``` yaml
---
date: 2024-01-31
pin: true
---

# Hello world!
...
```

如果有多个帖子被固定，它们将按创建日期排序，最近的固定帖子将首先显示，其余固定帖子将按降序显示。

#### 设置阅读时间 {#setting-the-reading-time}

当[启用]时，[readtime]包用于计算每篇帖子的预期阅读时间，该时间作为帖子和帖子摘要的一部分渲染。如今，许多博客显示阅读时间，这就是为什么[内置博客插件]也提供这个功能的原因。

然而，有时候，计算出的阅读时间可能感觉不准确，或者导致奇怪和不愉快的数字。因此，可以用前置元素 `readtime` 属性覆盖阅读时间并显式设置帖子的阅读时间：

``` yaml
---
date: 2024-01-31
readtime: 15
---

# Hello world!
...
```

这将禁用自动阅读时间计算。

  [readtime]: https://pypi.org/project/readtime/
  [启用]: ../plugins/blog.md#config.post_readtime

#### 设置默认值 {#setting-defaults}

<!-- md:sponsors -->
<!-- md:version insiders-4.21.0 -->
<!-- md:plugin [meta] – built-in -->
<!-- md:flag experimental -->

如果您有很多帖子，为每篇帖子定义所有上述内容可能会感觉重复。幸运的是，[内置元数据插件]允许按文件夹设置默认前置元素属性。您可以按分类或作者对您的帖子进行分组，并添加一个 `.meta.yml` 文件来设置通用属性：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ posts/
│     ├─ .meta.yml # (1)!
│     └─ index.md
└─ mkdocs.yml
```

1.  如已经指出的，您也可以在 `posts` 目录的嵌套文件夹中放置一个 `.meta.yml` 文件。此文件可以定义在帖子中有效的所有前置元素属性，例如：

    ``` yaml
    authors:
      - squidfunk
    categories:
      - Hello
      - World
    ```

请注意顺序很重要——[内置元数据插件]必须在 `mkdocs.yml` 中定义在博客插件之前，以便[内置博客插件]正确捕获所有设置的默认值：

``` yaml
plugins:
  - meta
  - blog
```

`.meta.yml` 文件中的列表和字典与为帖子定义的值合并和去重，这意味着您可以在 `.meta.yml` 中定义通用属性，然后为每篇帖子添加特定属性或覆盖。

  [内置元数据插件]: ../plugins/meta.md

### 添加页面 {#adding-pages}

除了帖子，通过在 `mkdocs.yml` 的[`nav`][nav]部分列出页面，也可以向您的博客添加静态页面。所有生成的索引都包含在最后指定的页面之后。例如，要在博客中添加关于博客作者的页面，请添加以下内容到 `mkdocs.yml` 中：

``` yaml
nav:
  - Blog:
    - blog/index.md
    - blog/authors.md
      ...
```

## 自定义 {#customization}

### 自定义索引页面 {#custom-index-pages}

<!-- md:sponsors -->
<!-- md:version insiders-4.24.0 -->
<!-- md:flag experimental -->

如果您想在自动生成的[归档]和[分类]索引中添加自定义内容，例如在帖子列表前添加分类描述，您可以手动创建[内置博客插件]将创建的类别页面的相同位置的文件：

``` { .sh .no-copy }
.
├─ docs/
│  └─ blog/
│     ├─ category/
│     │  └─ hello.md # (1)!
│     ├─ posts/
│     └─ index.md
└─ mkdocs.yml
```

1.  最简单的方法是首先[添加分类]到博客帖子，然后获取[内置博客插件]生成的 URL，并在[`blog_dir`][this is configurable]文件夹的相应位置创建文件。

    请注意，所示的目录列表基于默认配置。如果您为以下选项指定了不同的值，请确保相应调整路径：

    - [`blog_dir`][this is configurable]
    - [`categories_url_format`][categories_url_format]
    - [`categories_slugify`][categories_slugify]

您现在可以向新创建的文件添加任意内容，或为此页面设置特定的前置元素属性，例如更改[页面描述]：

``` yaml
---
description: Nullam urna elit, malesuada eget finibus ut, ac tortor.
---

# Hello
...
```

属于该分类的所有帖子摘要将自动附加。

  [添加分类]: #adding-categories
  [页面描述]: ../reference/index.md#setting-the-page-description
  [categories_url_format]: ../plugins/blog.md#config.categories_url_format
  [categories_slugify]: ../plugins/blog.md#config.categories_slugify

### 覆盖模板 {#overriding-templates}

[内置博客插件]建立在与 Material for MkDocs 相同的基础上，这意味着您可以使用[主题扩展]按照惯例覆盖博客使用的所有模板。

[内置博客插件]添加了以下模板：

- [`blog.html`][blog.html] – 博客、归档和分类索引的模板
- [`blog-post.html`][blog-post.html] – 博客帖子的模板

  [主题扩展]: ../customization.md#extending-the-theme

  [blog.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/blog.html
  [blog-post.html]: https://github.com/squidfunk/mkdocs-material/blob/master/src/templates/blog-post.html
