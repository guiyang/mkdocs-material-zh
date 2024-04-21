# Building an optimized site

Material for MkDocs 默认允许构建优化的网站，这些网站在搜索引擎上的排名表现优异，即使在慢速网络上也能快速加载，并且在没有 JavaScript 的情况下也能完美运行。此外，[内置优化插件]还增加了对更多有用的自动优化技术的支持。

  [内置优化插件]: #built-in-optimize-plugin

## 配置 {#configuration}

### 内置项目插件 {#built-in-projects-plugin}

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:plugin [projects] – built-in -->
<!-- md:flag experimental -->

内置项目插件允许您将文档分割为多个独立的 MkDocs 项目，__并发构建__ 并 __一起提供服务__。在 `mkdocs.yml` 中添加以下内容：

``` yaml
plugins:
  - projects
```

有关所有设置的列表，请查阅[插件文档]。

  [projects]: ../plugins/projects.md
  [插件文档]: ../plugins/projects.md

??? info "项目插件的用例"

    项目插件的理想用例包括：

    - 构建多语言站点
    - 在您的文档旁边构建博客
    - 为了更好的性能分割大型代码库

    请注意，该插件目前处于实验阶段。我们提前发布它，以便我们可以与用户一起改进它，并在我们发现新的用例时使其更加强大。

### 内置优化插件 {#built-in-optimize-plugin}

<!-- md:sponsors -->
<!-- md:version insiders-4.29.0 -->
<!-- md:plugin [optimize] – built-in -->
<!-- md:flag experimental -->

内置优化插件自动识别并在构建过程中使用压缩和转换技术优化所有媒体文件。在 `mkdocs.yml` 中添加以下行：

``` yaml
plugins:
  - optimize
```

有关所有设置的列表，请查阅[优化插件文档][optimize]。

  [optimize]: ../plugins/optimize.md
