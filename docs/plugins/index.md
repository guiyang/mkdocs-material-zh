# 内置插件 {#built-in-plugins}

Material for MkDocs 最初是作为 [MkDocs][mkdocs] 的一个主题开始的，但自那以后，它已发展成为一个完整的框架，用于构建和维护文档。主题仍然是项目的核心，但现在它伴随着越来越多的补充内置插件。

我们努力使这些插件尽可能模块化和通用，以便它们可以在各种项目和用例中使用。通过提供有用的默认设置，我们还尝试使它们尽可能易于使用，以便您可以快速开始，稍后再调整它们的设置。在开发内置插件时，我们始终遵循以下设计原则：

- **模块化:** 内置插件被设计为模块化的，因此它们可以轻松组合以实现复杂的流程。例如，[offline]、[optimize] 和 [privacy] 插件可以一起使用，构建真正的[离线可用文档]。

- **互操作性：** 内置插件被设计为尽可能兼容，因此它们可以与其他插件（包括第三方插件）组合使用。我们努力使其简单地与围绕 [MkDocs][mkdocs] 发展的庞大生态系统集成。

- **性能：** 内置插件被设计为尽可能快速和内存高效，以便它们不会不必要地减慢构建速度。这对于拥有数千页面的大型文档项目尤其重要。

  [mkdocs]: https://www.mkdocs.org/
  [design principles]: ../design-principles.md
  [离线可用文档]: ../setup/building-for-offline-usage.md

## 类别 {#categories}

### 管理 {#management}

以下插件极大地改善了在文档项目上工作时的编写体验，提供了更好的管理功能，从插件管理、多项目管理和元数据管理，到为错误报告创建最小复现：

<div class="grid cards" markdown>

-   :material-format-list-group: &nbsp; __[内置群组插件][group]__

    ---

    群组插件允许将插件分组为逻辑单元，以便使用[环境变量][mkdocs.env]为特定环境有条件地启用或禁用它们。

    ---

    __在不同环境中构建时优化插件管理__

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件便于管理文件夹中所有页面的元数据（前言），因此某些页面使用特定标签或自定义模板。

    ---

    __简化元数据的组织、分类和管理__

-   :material-folder-open: &nbsp; __[内置项目插件][projects]__

    ---

    项目插件允许将您的主项目拆分为多个独立的项目，同时构建并一起预览为一个整体。

    ---

    __连接多个项目在一起，分别或作为一个整体构建__

-   :material-information: &nbsp; __[内置信息插件][info]__

    ---

    信息插件是一个小而有用的工具，帮助创建自包含的最小复现，因此我们的维护人员可以更快地修复报告的错误。

    ---

    __您的错误报告质量最高，以便我们能尽快修复__


</div>

  [group]: group.md
  [info]: info.md
  [meta]: meta.md
  [projects]: projects.md

### 优化 {#optimization}

以下插件旨在帮助您构建优化的文档，通过更快的加载时间、更好的搜索引擎排名、在社交媒体上的美观预览图像和几行配置实现 GDPR 合规性，使其对用户更加可访问：

<div class="grid cards" markdown>

-   :material-share-circle: &nbsp; __[内置社交插件][social]__

    ---

    社交插件自动生成每个页面的美观且可定制的社交卡片，显示为社交媒体上的预览。

    ---

    __当在社交媒体上分享您的网站链接时，渲染美观的社交卡片__

-   :material-rabbit: &nbsp; __[内置优化插件][optimize]__

    ---

    优化插件自动识别并使用压缩和转换技术优化您项目中引用的所有媒体文件。

    ---

    __您的站点加载更快，因为为您的用户提供了更小的图片__

-   :material-shield-account: &nbsp; __[内置隐私插件][privacy]__

    ---

    隐私插件自动下载外部资产以便易于自托管，允许通过一行配置实现 GDPR 合规。

    ---

    __您的文档可以通过最小的努力实现 GDPR 合规__

-   :material-connection: &nbsp; __[内置离线插件][offline]__

    ---

    离线插件添加了构建[离线可用文档]的支持，因此您可以将 [`site` 目录][mkdocs.site_dir] 分发为可下载的 `.zip` 文件。

    ---

    __您的文档可以在没有互联网连接的情况下工作__

</div>

  [offline]: offline.md
  [optimize]: optimize.md
  [privacy]: privacy.md
  [social]: social.md

### 内容 {#content}

以下插件旨在帮助您设置博客，为用户提供搜索功能，向页面和帖子添加标签，并在文档的特定部分使用与主内容相同的排版能力：

<div class="grid cards" markdown>

-   :material-newspaper-variant-outline: &nbsp; __[内置博客插件][blog]__

    ---

    博客插件为 Material for MkDocs 添加了一流的博客支持，可以作为文档的侧车或作为独立安装。

    ---

    __您的博客使用与您的文档相同的强大引擎构建__

-   :material-magnify: &nbsp; __[内置搜索插件][search]__

    ---

    搜索插件在标题栏中添加了一个搜索栏，允许用户搜索整个文档，使他们更容易找到他们正在寻找的内容。

    ---

    __您的文档即使离线也可以搜索，无需任何外部服务__

-   :material-tag-text: &nbsp; __[内置标签插件][tags]__

    ---

    标签插件为使用标签对页面进行分类添加了一流的支持，增加了将相关页面分组以改善相关内容发现的能力。

    ---

    __您的页面通过标签进行分类，提供额外的上下文__

-   :material-format-title: &nbsp; __[内置排版插件][typeset]__

    ---

    排版插件允许在导航和目录中保留标题和标题的丰富展示。

    ---

    __侧边栏保留与页面中章节标题相同的格式__

</div>

  [blog]: blog.md
  [search]: search.md
  [tags]: tags.md
  [typeset]: typeset.md

## 架构 {#architecture}

### 多实例 {#multiple-instances}

几个内置插件支持多实例，这意味着它们可以在同一配置文件中多次使用，允许为项目的不同部分微调行为。目前，以下插件支持多实例：

<div class="mdx-columns" markdown>

- [内置博客插件][blog]
- [内置群组插件][group]
- [内置优化插件][optimize]
- [内置隐私插件][privacy]
- [内置社交插件][social]

</div>
