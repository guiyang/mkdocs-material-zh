# 约定

本节解释了本文档中使用的几种约定。

## 符号

本文档使用一些符号来进行说明。在继续阅读之前，请确保您已熟悉以下约定列表：

### <!-- md:sponsors --> – 仅限赞助者 { data-toc-label="仅限赞助者" }

跳动的心脏符号表示某个特定功能或行为仅对赞助者通过 [Insiders] 可用。如果您想使用该功能，请确保您有访问 [Insiders] 的权限。

### <!-- md:version --> – 版本 { data-toc-label="版本" }

标签符号与版本号一起使用，表示添加了特定的功能或行为的时间。如果您想使用它，请确保您至少在此版本上。

### <!-- md:version insiders- --> – 版本（Insiders） { data-toc-label="版本（Insiders）" }

标签符号与心形符号以及版本号一起使用，表示特定功能或行为已添加到 Material for MkDocs 的 [Insiders] 版本中。

### <!-- md:default --> – 默认值 { #default data-toc-label="默认值" }

`mkdocs.yml` 中的某些属性在作者没有明确定义时有默认值。属性的默认值总是包含在内。

#### <!-- md:default computed --> – 默认值是计算得出的 { #default data-toc-label="是计算得出的" }

一些默认值不是设置为静态值，而是根据其他值计算得出的，如站点语言、仓库提供者或其他设置。

#### <!-- md:default none --> – 默认值为空 { #default data-toc-label="为空" }

一些属性不包含默认值。这意味着，除非明确启用，否则与它们相关联的功能不可用。

### <!-- md:flag metadata --> – 元数据属性 { #metadata data-toc-label="元数据属性" }

此符号表示所描述的内容是元数据属性，可以在 Markdown 文档的前言定义中使用。

### <!-- md:flag multiple --> – 多实例 { #multiple-instances data-toc-label="多实例" }

此符号表示插件支持多实例，即可以在 `mkdocs.yml` 的 `plugins` 设置中多次使用。

### <!-- md:feature --> – 可选功能 { #feature data-toc-label="可选功能" }

大多数功能都隐藏在功能标志后面，这意味着必须通过 `mkdocs.yml` 明确启用它们。这允许存在潜在的正交功能。

### <!-- md:flag experimental --> – 实验性 { data-toc-label="实验性" }

一些较新的功能仍被视为实验性的，这意味着它们可能（尽管很少）随时更改，包括完全移除（尚未发生过）。

### <!-- md:plugin --> – 插件 { data-toc-label="插件" }

通过 MkDocs 出色的插件架构实现了几个功能，其中一些是内置的，并与 Material for MkDocs 一起分发，因此无需安装。

### <!-- md:extension --> – Markdown 扩展 { data-toc-label="Markdown 扩展" }

此符号表示所描述的内容是 Markdown 扩展，可以在 `mkdocs.yml` 中启用，并为 Markdown 解析器添加额外功能。

### <!-- md:flag required --> – 必需值 { #required data-toc-label="必需值" }

某些（实际上非常少）属性或设置是必需的，这意味着作者必须明确定义它们。

### <!-- md:flag customization --> – 自定义 { #customization data-toc-label="自定义" }

此符号表示所描述的内容是必须由作者添加的自定义。

### <!-- md:utility --> – 实用工具 { data-toc-label="实用工具" }

除了插件，还有一些实用工具建立在 MkDocs 之上，以提供扩展功能，例如支持版本控制。

  [Insiders]: insiders/index.md