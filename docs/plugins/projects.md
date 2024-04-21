---
title: 内置项目插件
icon: material/folder-open
---

# 内置项目插件 {#built-in-projects-plugin}

项目插件增加了将主项目拆分为多个独立项目、并行构建并作为一个整体预览的能力。这在创建多语言项目时特别有用，也可以用于将非常大的项目拆分为较小的部分。

---

<!-- md:sponsors --> <!-- md:sponsors --> __仅限赞助者__ — 此插件目前仅供[我们的优秀赞助者]使用。

  [我们的优秀赞助者]: ../insiders/index.md

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

该插件扫描配置的[`projects`目录][config.projects_dir]以查找`mkdocs.yml`文件，识别所有嵌套项目，并并行构建它们。如果没有另行配置，该插件预期您的项目具有以下目录布局，例如用于多语言项目：

``` { .sh .no-copy }
.
├─ docs/
├─ projects/
│  ├─ en/
│  │  ├─ docs/
│  │  └─ mkdocs.yml
│  └─ de/
│     ├─ docs/
│     └─ mkdocs.yml
└─ mkdocs.yml
```

该插件最有用和有趣的特性之一是它允许从主项目[预览您的站点]，同时仍能预览并单独构建每个项目。这对多语言项目特别有用。

如果在[预览您的站点]时，您更改了某个项目中的文件，插件只会重建此项目，并确保MkDocs也会重新加载相关文件。这也为将您的主项目拆分为几个项目创造了更好的编辑体验的机会。

有一些[限制]，但我们正在努力消除它们。

  [预览您的站点]: ../creating-your-site.md#previewing-as-you-write
  [limitations]: #limitations

### 何时使用它 {#when-to-use-it}

该插件的诞生是因为我们需要一种方便且可扩展的方法来构建我们的[示例]存储库，该存储库包含许多独立且可运行的项目，用户可以下载并用作启动新项目或[创建复现]时的基础。

当您想创建一个多语言项目，或者有一个非常大的现有项目时，您可能会考虑使用该插件，因为它使管理、编辑和构建变得更加舒适。

  [示例]: https://github.com/mkdocs-material/examples
  [创建复现]: ../guides/creating-a-reproduction.md

## 配置 {#configuration}

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:plugin [projects] – built-in -->
<!-- md:flag experimental -->

要开始使用项目插件，只需将以下行添加到`mkdocs.yml`中，并将您的主项目拆分为几个可以并行构建的独立项目：

``` yaml
plugins:
  - projects
```

项目插件已内置于Material for MkDocs中，无需安装。

  [projects]: projects.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。如果您想禁用插件，例如，对于本地构建，您可以在`mkdocs.yml`中使用[环境变量][mkdocs.env]：

``` yaml
plugins:
  - projects:
      enabled: !ENV [CI, false]
```

此配置仅在持续集成（CI）期间启用插件。

  [构建您的项目]: ../creating-your-site.md#building-your-site

---

#### <!-- md:setting config.concurrency -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default available CPUs - 1 -->

有更多的CPU可用时，插件可以并行处理更多工作，从而更快地构建项目。如果您想完全禁用并发处理，请使用：

``` yaml
plugins:
  - projects:
      concurrency: 1
```

默认情况下，插件使用所有可用的CPU - 1，最少为1。

### 缓存 {#caching}

插件实现了一个[智能缓存]机制，确保只有在其内容发生变化时才重新构建项目。虽然初始构建可能需要一些时间，但使用缓存是个好主意，因为它会加快连续构建的速度。

以下设置可用于缓存：

  [智能缓存]: requirements/caching.md

---

#### <!-- md:setting config.cache -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `true` -->

使用此设置指示插件绕过缓存，以重建所有项目，即使缓存可能并未过期。通常不需要指定此设置，除非在调试插件本身时。可以使用以下方法禁用缓存：

``` yaml
plugins:
  - projects:
      cache: false
```

---

#### <!-- md:setting config.cache_dir -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `.cache/plugin/projects` -->

通常不需要指定此设置，除非您想更改根目录内元数据缓存的路径。如果您想更改它，请使用：

``` yaml
plugins:
  - projects:
      cache_dir: my/custom/dir
```

### 日志记录 {#logging}

以下设置可用于日志记录：

---

#### <!-- md:setting config.log -->

<!-- md:sponsors -->
<!-- md:version insiders-4.47.0 -->
<!-- md:default `true` -->

使用此设置控制插件在构建站点时是否应显示项目的日志消息。虽然不推荐，但您可以禁用日志记录：

``` yaml
plugins:
  - projects:
      log: false
```

---

#### <!-- md:setting config.log_level -->

<!-- md:sponsors -->
<!-- md:version insiders-4.47.0 -->
<!-- md:default `info` -->

使用此设置控制插件在遇到错误时应使用的日志级别，这要求启用[`log`][config.log]设置。以下日志级别可用：

=== "`error`"

    ``` yaml
    plugins:
      - projects:
          log_level: error
    ```

    仅报告错误。

=== "`warn`"

    ``` yaml
    plugins:
      - projects:
          log_level: warn
    ```

    报告错误和警告，在[`strict`][mkdocs.strict]模式下终止构建。

=== "`info`"

    ``` yaml
    plugins:
      - projects:
          log_level: info
    ```

    报告错误、警告和信息性消息。

=== "`debug`"

    ``` yaml
    plugins:
      - projects:
          log_level: debug
    ```

    报告所有消息，包括调试消息。

### 项目 {#projects}

以下设置可用于项目：

---

#### <!-- md:setting config.projects -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用项目的构建。目前，插件的唯一目的是构建项目，因此等同于[`enabled`][config.enabled]设置，但未来可能会添加其他功能。如果您想禁用项目的构建，请使用：

``` yaml
plugins:
  - projects:
      projects: false
```

---

#### <!-- md:setting config.projects_dir -->

<!-- md:sponsors -->
<!-- md:version insiders-4.38.0 -->
<!-- md:default `projects` -->

使用此设置更改项目所在的文件夹。通常不需要更改此设置，但如果您想重命名文件夹或更改其文件系统位置，请使用：

``` yaml
plugins:
  - projects:
      projects_dir: projects
```

请注意，[`projects`目录][config.projects_dir]仅用于项目组织 - 它不包括在项目URL中，因为项目会由插件自动提升。

提供的路径从根目录解析。

---

#### <!-- md:setting config.projects_config_files -->

<!-- md:sponsors -->
<!-- md:version insiders-4.42.0 -->
<!-- md:default `*/mkdocs.yml` -->

使用此设置更改插件在扫描[`projects`目录][config.projects_dir]时查找的配置文件的位置或名称。调整此设置可能是必要的，当配置文件位于项目的子目录中，例如`docs/mkdocs.yml`：

``` yaml
plugins:
  - projects:
      projects_config_files: "**/mkdocs.yml" # (1)!
```

1.  如果所有项目的配置文件都位于同一位置，例如，`docs/mkdocs.yml`，建议完全限定路径，因为它比`**`通配符模式解析得更快。

    ``` yaml
    plugins:
      - projects:
          projects_config_files: "*/docs/mkdocs.yml"
    ```

    此配置适用于以下目录结构，这对于使用git子模块的项目而言相当常见：

    ``` { .sh .no-copy }
    .
    ├─ docs/
    ├─ projects/
    │  ├─ git-submodule-a/
    │  │  └─ docs/
    │  │     └─ mkdocs.yml
    │  └─ git-submodule-b/
    │     └─ docs/
    │        └─ mkdocs.yml
    └─ mkdocs.yml
    ```

提供的路径从[`projects`目录][config.projects_dir]解析。

---

#### <!-- md:setting config.projects_config_transform -->

<!-- md:sponsors -->
<!-- md:version insiders-4.42.0 -->
<!-- md:default none -->

使用此设置在构建之前转换从`mkdocs.yml`读取的每个项目的配置，这允许在一起构建时调整每个项目的配置，但在单独构建时保持不变：

``` yaml
plugins:
  - projects:
      projects_config_transform: !!python/name:projects.transform
```

提供的模块和函数名称在Python的[模块搜索路径]中查找。您需要在构建站点时将根目录添加到搜索路径中，以便Python可以解析它。最简单的方法是将工作目录添加到[`PYTHONPATH`][PYTHONPATH]环境变量中：

``` .sh
export PYTHONPATH=.
```

!!! tip "如何定义配置转换函数"

    [`python/name`][python-name]标签由[PyYAML]提供，并必须指向Python的[模块搜索路径]中的有效模块和函数名称。插件将`project`和顶级`config`对象传递给函数。

    例如，我们可以从顶级配置继承[`use_directory_urls`][mkdocs.use_directory_urls]设置，适用于所有项目：

    ``` py title="projects/__init__.py"
    from mkdocs.config.defaults import MkDocsConfig

    # Transform project configuration
    def transform(project: MkDocsConfig, config: MkDocsConfig):
        project.use_directory_urls = config.use_directory_urls
    ```

  [模块搜索路径]: https://docs.python.org/3/library/sys_path_init.html
  [PYTHONPATH]: https://docs.python.org/3/using/cmdline.html#envvar-PYTHONPATH
  [python-name]: https://pyyaml.org/wiki/PyYAMLDocumentation#yaml-tags-and-python-types
  [PyYAML]: https://pyyaml.org/

### 提升 {#hoisting}

以下设置可用于提升：

---

#### <!-- md:setting config.hoisting -->

<!-- md:sponsors -->
<!-- md:version insiders-4.39.0 -->
<!-- md:default `true` -->

使用此设置启用或禁用将主题文件提升到主项目的能力。如果您禁用此设置，则每个项目将收到主题文件的副本，这可能被视为多余的：

``` yaml
plugins:
  - projects:
      hoisting: false
```

通常建议启用提升，因为它可以加快项目站点的部署和加载速度，因为所有项目的文件都是相同的，可以去重。

### 限制 {#limitations}

该插件是Material for MkDocs的最新添加之一，这意味着它相对年轻，并且有一些限制。我们正在努力消除这些限制，并且我们很乐意收到反馈并了解您的需求，以便?5800。当前的限制包括：

- __仅基本多语言支持__：我们将研究如何为多语言项目提供更好的支持，使得项目之间的互联和切换变得更容易。

- __独立的搜索索引和站点地图__：当前，项目是完全独立的，这意味着它们将有独立的搜索索引和站点地图。