---
title: 内置搜索插件
icon: material/magnify
---

# 内置搜索插件 {#built-in-search-plugin}

搜索插件在头部添加了一个搜索栏，允许用户搜索您的文档。它由 [lunr.js] 驱动，这是一个轻量级的浏览器全文搜索引擎，无需外部服务，并且在构建[离线可用文档]时也能工作。

  [lunr.js]: https://lunrjs.com/
  [离线可用文档]: ../setup/building-for-offline-usage.md

## 目标 {#objective}

### 它是如何工作的 {#how-it-works}

插件扫描生成的HTML并从所有页面和部分中构建搜索索引，通过提取章节标题和内容。它保留了一些内联格式，如代码块和列表，但移除了所有其他格式，使搜索索引尽可能小。

当用户访问您的站点时，搜索索引被发送到浏览器，用 [lunr.js] 索引并可用于快速简单的查询 — 无需服务器。这确保了搜索索引始终与您的文档保持同步，提供准确的结果。

### 何时使用它 {#when-to-use-it}

通常建议使用该插件，因为交互式搜索功能是每个优秀文档的重要部分。此外，该插件与 Material for MkDocs 提供的其他[内置插件]完美集成：

<div class="grid cards" markdown>

-   :material-connection: &nbsp; __[内置离线插件][offline]__

    ---

    离线插件增加了构建离线可用文档的支持，因此您可以将[`site`目录][mkdocs.site_dir]作为可下载的`.zip`文件分发。

    ---

    __您的文档可以在没有互联网连接的情况下工作__

-   :material-file-tree: &nbsp; __[内置元数据插件][meta]__

    ---

    元数据插件使得在搜索结果中[提升][meta.search.boost]特定部分或[排除][meta.search.exclude]它们完全不被索引变得容易，从而对搜索进行更细致的控制。

    ---

    __简化不同子部分搜索的组织和管理__

</div>

  [offline]: offline.md
  [meta]: meta.md
  [内置插件]: index.md

## 配置 {#configuration}

<!-- md:version 9.0.0 -->
<!-- md:plugin [search] – built-in -->

与所有[内置插件]一样，开始使用搜索插件非常简单。只需将以下行添加到`mkdocs.yml`，您的用户就能搜索您的文档：

``` yaml
plugins:
  - search
```

搜索插件已内置于Material for MkDocs中，无需安装。

  [search]: search.md
  [内置插件]: index.md

### 通用 {#general}

以下设置可用：

---

#### <!-- md:setting config.enabled -->

<!-- md:version 9.2.9 -->
<!-- md:default `true` -->

使用此设置在[构建您的项目]时启用或禁用插件。通常不需要指定此设置，但如果您想禁用插件，请使用：

``` yaml
plugins:
  - search:
      enabled: false
```

  [构建您的项目]: ../creating-your-site.md#building-your-site

### 搜索 {#search}

以下设置适用于搜索：

---

#### <!-- md:setting config.lang -->

<!-- md:version 9.0.0 -->
<!-- md:default computed -->

使用此设置指定搜索索引的语言，支持除英语以外的其他语言的[词干提取]。默认值会自动从[站点语言]计算，但也可以显式设置为另一种语言或多种语言：

=== "设置语言"

    ``` yaml
    plugins:
      - search:
          lang: en
    ```

=== "添加更多语言"

    ``` yaml
    plugins:
      - search:
          lang: # (1)!
            - en
            - de
    ```

    1.  请注意，包括对其他语言的支持会增加约20kb的基础JavaScript负载，并且每种语言再增加15-30kb，以上都是在`gzip`之前。

  [词干提取]: https://en.wikipedia.org/wiki/Stemming
  [站点语言]: ../setup/changing-the-language.md#site-language
  [lunr languages]: https://github.com/MihaiValentin/lunr-languages

语言支持由 [lunr languages] 提供，这是一个由开源社区维护的 [lunr.js] 的特定语言词干器和停用词集合。

---

目前 [lunr languages] 支持以下语言：

<div class="mdx-columns" markdown>

- `ar` – Arabic
- `da` – Danish
- `de` – German
- `du` – Dutch
- `en` – English
- `es` – Spanish
- `fi` – Finnish
- `fr` – French
- `hi` – Hindi
- `hu` – Hungarian
- `hy` – Armenian
- `it` – Italian
- `ja` – Japanese
- `kn` - Kannada
- `ko` – Korean
- `no` – Norwegian
- `pt` – Portuguese
- `ro` – Romanian
- `ru` – Russian
- `sa` – Sanskrit
- `sv` – Swedish
- `ta` – Tamil
- `te` – Telugu
- `th` – Thai
- `tr` – Turkish
- `vi` – Vietnamese
- `zh` – Chinese

</div>

如果 [lunr languages] 未为选定的[站点语言]提供支持，插件将回退到提供最佳词干提取结果的另一种语言。如果您发现搜索结果不令人满意，您可以通过为您的语言添加支持来为 [lunr languages] 做出贡献。

---

#### <!-- md:setting config.separator -->

<!-- md:version 9.0.0 -->
<!-- md:default computed -->

使用此设置指定在客户端构建搜索索引时用于拆分单词的分隔符。默认值会自动从[站点语言]计算，但也可以显式设置为另一个值：

``` yaml
plugins:
  - search:
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
```

分隔符支持[前瞻和后顾断言]，这允许使用相当复杂的表达式，以精确控制在构建搜索索引时如何拆分单词。

将其拆分为各个部分，此分隔符引发以下行为：

=== "特殊字符"

    ```
    [\s\-,:!=\[\]()"/]+
    ```

    表达式的第一部分在每个文档中的空格、连字符、逗号、括号和其他特殊字符前后插入标记边界。如果这些特殊字符相邻，则视为一个。

=== "大小写变化"

    ```
    (?!\b)(?=[A-Z][a-z])
    ```

    许多编程语言有`PascalCase`或`camelCase`等命名约定。通过在分隔符中添加此子表达式，[在大小写变化处拆分单词]，将单词`PascalCase`拆分为`Pascal`和`Case`。

=== "版本字符串"

    ```
    \.(?!\d)
    ```

    添加`.`到分隔符时，像`1.2.3`这样的版本字符串会被拆分为`1`、`2`和`3`，使它们无法通过搜索找到。使用此子表达式时，引入了一个小的前瞻，将[保留版本字符串]并保持其可搜索性。

=== "HTML/XML标签"

    ```
    &[lg]t;
    ```

    如果您的文档包含HTML/XML代码示例，您可能希望允许用户查找[特定标签名称]。不幸的是，`<`和`>`控制字符在代码块中编码为`&lt;`和`&gt;`。将此子表达式添加到分隔符中就是为了这个目的。

  [前瞻和后顾断言]: https://www.regular-expressions.info/lookaround.html
  [在大小写变化处拆分单词]: ?q=searchHighlight
  [保留版本字符串]: ?q=9.0.0
  [specific tag names]: ?q=script

---

#### <!-- md:setting config.pipeline -->

<!-- md:version 9.0.0 -->
<!-- md:default computed -->
<!-- md:flag experimental -->

使用此设置指定在使用[`separator`][config.separator]对其进行标记化并在将其添加到搜索索引之前用于过滤和扩展标记的[管道函数]。默认值会自动从[站点语言]计算，但也可以显式设置：

``` yaml
plugins:
  - search:
      pipeline:
        - stemmer
        - stopWordFilter
        - trimmer
```

可用的管道函数包括：

- `stemmer` – 将标记词干化为其根形式，例如 `running` 到 `run`
- `stopWordFilter` – 根据常见词过滤，例如 `a`、`the` 等。
- `trimmer` – 从标记中修剪空格

  [管道函数]: https://lunrjs.com/guides/customising.html#pipeline-functions

### 分词 {#segmentation}

该插件支持通过 [jieba]，一个流行的中文文本分词库，对中文进行文本分词。其他语言如日语和韩语目前在客户端进行分词，但我们正在考虑将来将此功能移入插件。

以下设置可用于分词：

  [jieba]: https://pypi.org/project/jieba/

---

#### <!-- md:setting config.jieba_dict -->

<!-- md:version 9.2.0 -->
<!-- md:default none -->
<!-- md:flag experimental -->

使用此设置指定[jieba]用于分词的[自定义词典]，替换默认词典。[jieba]自带几个词典，可以使用：

``` yaml
plugins:
  - search:
      jieba_dict: dict.txt
```

[jieba]提供以下词典：

- [dict.txt.small] – 占用内存较小的词典文件
- [dict.txt.big] – 支持繁体分词更好的词典文件

提供的路径从根目录解析。

  [custom dictionary]: https://github.com/fxsjy/jieba#%E5%85%B6%E4%BB%96%E8%AF%8D%E5%85%B8
  [dict.txt.small]: https://github.com/fxsjy/jieba/raw/master/extra_dict/dict.txt.small
  [dict.txt.big]: https://github.com/fxsjy/jieba/raw/master/extra_dict/dict.txt.big

---

#### <!-- md:setting config.jieba_dict_user -->

<!-- md:version 9.2.0 -->
<!-- md:default none -->
<!-- md:flag experimental -->

使用此设置指定[jieba]用于分词的[用户词典]，增强默认词典。用户词典非常适合调整分词器：

``` yaml
plugins:
  - search:
      jieba_dict_user: user_dict.txt
```

提供的路径从根目录解析。

  [用户词典]: https://github.com/fxsjy/jieba#%E8%BD%BD%E5%85%A5%E8%AF%8D%E5%85%B8

## 使用方法 {#usage}

### 元数据 {#metadata}

以下属性可用：

---

#### <!-- md:setting meta.search.boost -->

<!-- md:version 8.3.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性增加或减少搜索结果中页面的相关性，给予它们更大的权重。使用大于 `1` 的值来提升排名，使用小于 `1` 的值来降低排名：

=== ":material-arrow-up-circle: 提升排名"

    ``` yaml
    ---
    search:
      boost: 2 # (1)!
    ---

    # Page title
    ...
    ```

    提升页面时，始终从低值开始。

=== ":material-arrow-down-circle: 降低排名"

    ``` yaml
    ---
    search:
      boost: 0.5
    ---

    # Page title
    ...
    ```

---

#### <!-- md:setting meta.search.exclude -->

<!-- md:version 9.0.0 -->
<!-- md:flag metadata -->
<!-- md:default none -->

使用此属性从搜索结果中排除一个页面。请注意，这不仅会移除页面，还会从搜索结果中移除该页面的所有子部分：

``` yaml
---
search:
  exclude: true
---

# Page title
...
```
