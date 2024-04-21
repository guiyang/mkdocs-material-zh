# 添加 Git 仓库 {#adding-a-git-repository}

如果您的文档与源代码相关，Material for MkDocs 提供了在静态站点中展示项目仓库信息的能力，包括星标和分叉数。此外，还可以显示[最后更新和创建日期]以及[贡献者]。

## 配置 {#configuration}

### 仓库 {#repository}

<!-- md:version 0.1.0 -->
<!-- md:default none -->

为了在文档中显示项目仓库的链接，请在 `mkdocs.yml` 中设置 [`repo_url`][repo_url] 为您的仓库的公开 URL，例如：

``` yaml
repo_url: https://github.com/squidfunk/mkdocs-material
```

在大屏幕上，仓库链接将呈现在搜索栏旁边，在较小的屏幕尺寸上则显示在主导航抽屉中。此外，对于托管在 [GitHub] 或 [GitLab] 上的公开仓库，会自动请求并呈现星标和分叉数。

GitHub 仓库还将包括最新发布版本的标签。[^1]

  [^1]:
    不幸的是，GitHub 只提供了获取[最新发布版本]的 API 端点 - 而不是最新标签。因此，请确保为您希望在星标和分叉数旁边显示的最新标签[创建一个发布版本]（不是预发布版本）。

  [repo_url]: https://www.mkdocs.org/user-guide/configuration/#repo_url
  [最新发布版本]: https://docs.github.com/en/rest/reference/releases#get-the-latest-release
  [创建一个发布版本]: https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release

#### 仓库名称 {#repository-name}

<!-- md:version 0.1.0 -->
<!-- md:default _automatically set to_ `GitHub`, `GitLab` _or_ `Bitbucket` -->

MkDocs 会通过检查 URL 来推断源提供者，并尝试自动设置 _仓库名称_。如果您希望自定义名称，请在 `mkdocs.yml` 中设置 [`repo_name`][repo_name]：

``` yaml
repo_name: squidfunk/mkdocs-material
```

  [repo_name]: https://www.mkdocs.org/user-guide/configuration/#repo_name

#### 仓库图标 {#repository-icon}

<!-- md:version 5.0.0 -->
<!-- md:default computed -->

虽然默认的仓库图标是一个通用的 git 图标，但可以通过在 `mkdocs.yml` 中引用有效的图标路径来设置为任何与主题捆绑的图标：

``` yaml
theme:
  icon:
    repo: fontawesome/brands/git-alt # (1)!
```

1.  输入几个关键词以使用我们的[图标搜索]找到完美的图标，并点击短代码将其复制到您的剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="git" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

一些流行的选择：

- :fontawesome-brands-git: – `fontawesome/brands/git`
- :fontawesome-brands-git-alt: – `fontawesome/brands/git-alt`
- :fontawesome-brands-github: – `fontawesome/brands/github`
- :fontawesome-brands-github-alt: – `fontawesome/brands/github-alt`
- :fontawesome-brands-gitlab: – `fontawesome/brands/gitlab`
- :fontawesome-brands-gitkraken: – `fontawesome/brands/gitkraken`
- :fontawesome-brands-bitbucket: – `fontawesome/brands/bitbucket`
- :fontawesome-solid-trash: – `fontawesome/solid/trash`

  [图标搜索]: ../reference/icons-emojis.md#search

#### Code actions {#code-actions}

<!-- md:version 9.0.0 -->
<!-- md:feature -->

如果 [repository URL] 指向一个有效的 [GitHub]、[GitLab] 或 [Bitbucket] 仓库，[MkDocs] 提供了一个名为 [`edit_uri`][edit_uri] 的设置，它解析到托管您文档的子文件夹。

如果您的默认分支名为 `main`，请更改设置：

``` yaml
edit_uri: edit/main/docs/
```

确保 `edit_uri` 配置正确后，可以添加代码操作按钮。支持两种类型的代码操作：`edit` 和 `view`（仅限 GitHub）：

=== ":material-file-edit-outline: 编辑此页面"

    ``` yaml
    theme:
      features:
        - content.action.edit
    ```

=== ":material-file-eye-outline: 查看此页面的源代码"

    ``` yaml
    theme:
      features:
        - content.action.view
    ```

可以使用以下行更改编辑和查看按钮的图标：

``` yaml
theme:
  icon:
    edit: material/pencil # (1)!
    view: material/eye
```

1.  输入几个关键词以使用我们的[图标搜索]找到完美的图标，并点击短代码将其复制到您的剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="material pencil" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

  [repository URL]: #repository
  [GitHub]: https://github.com/
  [GitLab]: https://about.gitlab.com/
  [Bitbucket]: https://bitbucket.org/
  [MkDocs]: https://www.mkdocs.org
  [edit_uri]: https://www.mkdocs.org/user-guide/configuration/#edit_uri

### 版本控制 {#revisioning}

以下插件与 Material for MkDocs 完全集成，允许显示文档的[最后更新和创建日期]，以及涉及的所有[贡献者]或[作者]的链接。

  [最后更新和创建日期]: #document-dates
  [贡献者]: #document-contributors
  [authors]: #document-authors

#### 文档日期 {#document-dates}

<!-- md:version 4.6.0 -->
<!-- md:plugin [git-revision-date-localized] -->

[git-revision-date-localized] 插件支持在每个页面的底部添加文档的最后更新和创建日期。使用 `pip` 安装它：

```
pip install mkdocs-git-revision-date-localized-plugin
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - git-revision-date-localized:
      enable_creation_date: true
```

支持以下配置选项：

<!-- md:option git-revision-date-localized.enabled -->

:   <!-- md:default `true` --> 此选项指定构建项目时是否启用插件。如果您想在本地构建时关闭插件，请使用[环境变量]：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          enabled: !ENV [CI, false]
    ```

<!-- md:option git-revision-date-localized.type -->

:   <!-- md:default `date` --> 要显示的日期格式。有效值包括 `date`、`datetime`、`iso_date`、`iso_datetime` 和 `timeago`：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          type: date
    ```

<!-- md:option git-revision-date-localized.enable_creation_date -->

:   <!-- md:default `false` --> 启用在页面底部最后更新日期旁显示与页面相关联的文件的创建日期：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          enable_creation_date: true
    ```

    !!! note "使用构建环境时"

        如果您通过 CI 系统部署，您可能需要在获取代码时调整您的 CI 设置。有关更多信息，请查看 [git-revision-date-localized]。

<!-- md:option git-revision-date-localized.fallback_to_build_date -->

:   <!-- md:default `false` --> 启用回退到执行 `mkdocs build` 的时间。当在非 git 仓库外进行构建时可以使用此选项作为回退：

    ``` yaml
    plugins:
      - git-revision-date-localized:
          fallback_to_build_date: true
    ```

此扩展的其他配置选项没有得到 Material for MkDocs 的官方支持，因此可能会产生意外结果。请自行决定使用。

  [git-revision-date-localized]: https://github.com/timvink/mkdocs-git-revision-date-localized-plugin

#### 文档贡献者 {#document-contributors}

<!-- md:version 9.5.0 -->
<!-- md:plugin [git-committers] -->
<!-- md:flag experimental -->

[git-committers][^2] 插件渲染所有贡献者的 GitHub 头像，并在每个页面的底部链接到他们的 GitHub 个人资料。一如既往，可以通过 `pip` 安装它：

  [^2]:
    我们目前建议使用 [git-committers] 插件的一个分支，因为它包含许多尚未合并回原始插件的改进。有关更多信息，请查看 byrnereese/mkdocs-git-committers-plugin#12。

```
pip install mkdocs-git-committers-plugin-2
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - git-committers:
      repository: squidfunk/mkdocs-material
      branch: main
```

支持以下配置选项：

<!-- md:option git-committers.enabled -->

:   <!-- md:default `true` --> 此选项指定构建项目时是否启用插件。如果您想在本地构建时关闭插件，请使用[环境变量]：

    ``` yaml
    plugins:
      - git-committers:
          enabled: !ENV [CI, false]
    ```

<!-- md:option git-committers.repository -->

:   <!-- md:default none --> <!-- md:flag required --> 必须设置此属性为包含您文档的仓库的 slug。slug 必须遵循 `<username>/<repository>` 的模式：

    ``` yaml
    plugins:
      - git-committers:
          repository: squidfunk/mkdocs-material
    ```

<!-- md:option git-committers.branch -->

:   <!-- md:default `master` --> 此属性应设置为从中检索贡献者的仓库分支。要使用 `main` 分支：

    ``` yaml
    plugins:
      - git-committers:
          branch: main
    ```

此扩展的其他配置选项没有得到 Material for MkDocs 的官方支持，因此可能会产生意外结果。请自行决定使用。

  [Insiders]: ../insiders/index.md
  [git-committers]: https://github.com/ojacques/mkdocs-git-committers-plugin-2
  [环境变量]: https://www.mkdocs.org/user-guide/configuration/#environment-variables
  [rate limits]: https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting

#### 文档作者 {#document-authors}

<!-- md:version 9.5.0 -->
<!-- md:plugin [git-authors] -->
<!-- md:flag experimental -->

[git-authors] 插件是 [git-committers] 插件的轻量级替代品，它从 git 中提取文档的作者，并在每个页面的底部显示它们。

Material for MkDocs 为 [git-authors] 提供了深度集成。这意味着不需要[自定义覆盖](https://timvink.github.io/mkdocs-git-authors-plugin/usage.html#mkdocs-material-theme)，并且添加了额外的样式（如漂亮的图标）。只需通过 `pip` 安装它：

```
pip install mkdocs-git-authors-plugin
```

然后，在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - git-authors
```

  [git-authors]: https://github.com/timvink/mkdocs-git-authors-plugin/
