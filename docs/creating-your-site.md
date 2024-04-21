# 创建新站点 {#creating-your-site}

在您已经[安装]了 Material for MkDocs 之后，可以使用 `mkdocs` 可执行文件来启动您的项目文档。转到您希望项目位于的目录，并输入：

```
mkdocs new .
```

如果您在 Docker 中运行 Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .
    ```

=== "Windows (cmd)"

    ```
    docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material new .
    ```

这将创建以下结构：

``` { .sh .no-copy }
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

  [安装]: getting-started.md

## 配置 {#configuration}

### 最小配置 {#minimal-configuration}

只需在 `mkdocs.yml` 中添加以下行来启用主题：

``` yaml
theme:
  name: material
```

  [installation methods]: getting-started.md#installation

???+ tip "推荐：[配置验证和自动补全]"

    为了最小化摩擦并最大化生产力，Material for MkDocs 提供了自己的 `mkdocs.yml` 的 [schema.json][^1]。如果您的编辑器支持 YAML schema 验证，强烈推荐设置它：

    === "Visual Studio Code"

        1.  安装 [`vscode-yaml`][vscode-yaml] 以支持 YAML 语言。
        2.  在您的用户或工作区的 [`settings.json`][settings.json] 中添加 schema，将其放在 `yaml.schemas` 键下：

            ``` json
            {
              "yaml.schemas": {
                "https://squidfunk.github.io/mkdocs-material/schema.json": "mkdocs.yml"
              },
              "yaml.customTags": [ // (1)!
                "!ENV scalar",
                "!ENV sequence",
                "!relative scalar",
                "tag:yaml.org,2002:python/name:material.extensions.emoji.to_svg",
                "tag:yaml.org,2002:python/name:material.extensions.emoji.twemoji",
                "tag:yaml.org,2002:python/name:pymdownx.superfences.fence_code_format"
              ]
            }
            ```

            1.  如果您计划使用 [图标和表情]，此设置是必需的，否则 Visual Studio Code 将在某些行显示错误。

    === "其他"

        1.  确保您选择的编辑器支持 YAML schema 验证。
        2.  在 `mkdocs.yml` 的顶部添加以下行：

            ``` yaml
            # yaml-language-server: $schema=https://squidfunk.github.io/mkdocs-material/schema.json
            ```

  [^1]:
    如果您是 MkDocs 插件或 Markdown 扩展的作者，而且您的项目与 Material for MkDocs 兼容，我们非常欢迎您在 GitHub 上通过拉取请求贡献一个针对您的 [extension] 或 [plugin] 的 schema。如果您已经定义了 schema，或希望自行托管您的 schema 以减少重复，您可以通过 [$ref] 添加它。

  [配置验证和自动补全]: https://twitter.com/squidfunk/status/1487746003692400642
  [schema.json]: schema.json
  [vscode-yaml]: https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml
  [settings.json]: https://code.visualstudio.com/docs/getstarted/settings
  [extension]: https://github.com/squidfunk/mkdocs-material/tree/master/docs/schema/extensions
  [plugin]: https://github.com/squidfunk/mkdocs-material/tree/master/docs/schema/plugins
  [$ref]: https://json-schema.org/understanding-json-schema/structuring.html#ref
  [icons and emojis]: reference/icons-emojis.md
  [图标和表情]: reference/icons-emojis.md

### 高级配置 {#advanced-configuration}

Material for MkDocs 提供了许多配置选项。设置部分详细解释了如何配置和自定义颜色、字体、图标等：

<div class="mdx-columns" markdown>

- [更改颜色]
- [更改字体]
- [更改语言]
- [更改 logo 和图标]
- [确保数据隐私]
- [设置导航]
- [设置站点搜索]
- [设置站点分析]
- [设置社交卡片]
- [设置博客]
- [设置标签]
- [设置版本]
- [设置页眉]
- [设置页脚]
- [添加 Git 仓库]
- [添加评论系统]
- [构建优化站点]
- [为离线使用构建]

</div>

此外，请查看与 Material for MkDocs 原生集成的支持的 [Markdown 扩展]，提供了前所未有的低努力技术写作体验。

  [更改颜色]: setup/changing-the-colors.md
  [更改字体]: setup/changing-the-fonts.md
  [更改语言]: setup/changing-the-language.md
  [更改 logo 和图标]: setup/changing-the-logo-and-icons.md
  [确保数据隐私]: setup/ensuring-data-privacy.md
  [设置导航]: setup/setting-up-navigation.md
  [设置站点搜索]: setup/setting-up-site-search.md
  [设置站点分析]: setup/setting-up-site-analytics.md
  [设置社交卡片]: setup/setting-up-social-cards.md
  [设置博客]: setup/setting-up-a-blog.md
  [设置标签]: setup/setting-up-tags.md
  [设置版本]: setup/setting-up-versioning.md
  [设置页眉]: setup/setting-up-the-header.md
  [设置页脚]: setup/setting-up-the-footer.md
  [添加 Git 仓库]: setup/adding-a-git-repository.md
  [添加评论系统]: setup/adding-a-comment-system.md
  [构建优化站点]: setup/building-an-optimized-site.md
  [为离线使用构建]: setup/building-for-offline-usage.md
  [Markdown 扩展]: setup/extensions/index.md

## 编辑中同步预览 {#previewing-as-you-write}

MkDocs 包括一个实时预览服务器，因此您可以在编写文档时预览更改。服务器将在保存时自动重建站点。启动它：

``` sh
mkdocs serve # (1)!
```

1.  如果您有一个大型文档项目，MkDocs 重建所有页面以供预览可能需要几分钟。如果您只对当前页面感兴趣，[`--dirtyreload`][--dirtyreload] 标志将使重建更快：

    ```
    mkdocs serve --dirtyreload
    ```

如果您在 Docker 中运行 Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
    ```

=== "Windows"

    ```
    docker run --rm -it -p 8000:8000 -v "%cd%":/docs squidfunk/mkdocs-material
    ```

在浏览器中访问 [localhost:8000][实时预览]，您应该会看到：

[![Creating your site]][Creating your site]

  [--dirtyreload]: https://www.mkdocs.org/about/release-notes/#support-for-dirty-builds-990
  [实时预览]: http://localhost:8000
  [Creating your site]: assets/screenshots/creating-your-site.png

## 构建您的站点 {#building-your-site}

当您完成编辑后，可以从您的 Markdown 文件构建一个静态站点：

```
mkdocs build
```

如果您在 Docker 中运行 Material for MkDocs，请使用：

=== "Unix, Powershell"

    ```
    docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material build
    ```

=== "Windows"

    ```
    docker run --rm -it -v "%cd%":/docs squidfunk/mkdocs-material build
    ```

此目录的内容构成了您的项目文档。无需操作数据库或服务器，因为它是完全独立的。该站点可以托管在 [GitHub 页面]、[GitLab 页面]、您选择的 CDN 或您的私人网络空间上。

  [GitHub 页面]: publishing-your-site.md#github-pages
  [GitLab 页面]: publishing-your-site.md#gitlab-pages

如果您打算将您的文档作为一组文件分发，以便从本地文件系统而不是 Web 服务器（如在 `.zip` 文件中）读取，请阅读关于[为离线使用构建]的注意事项。

  [为离线使用构建]: setup/building-for-offline-usage.md
