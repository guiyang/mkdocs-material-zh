---
icon: material/tab
---

# 内容标签页 Content tabs {#content-tabs}

有时，将不同的内容分组到不同的标签页下是很有必要的，例如在描述如何从不同的语言或环境访问API时。Material for MkDocs 允许创建美观且功能全面的标签页，可以分组代码块和其他内容。

## 配置 {#configuration}

此配置启用内容标签页，并允许在内容标签页中嵌套任意内容，包括代码块和更多内容标签页！将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.superfences
  - pymdownx.tabbed:
      alternate_style: true
```

查看其他配置选项：

- [SuperFences]
- [Tabbed]

  [SuperFences]: ../setup/extensions/python-markdown-extensions.md#superfences
  [Tabbed]: ../setup/extensions/python-markdown-extensions.md#tabbed

### 锚链接 {#anchor-links}

<!-- md:version 9.5.0 -->
<!-- md:flag experimental -->

为了链接到内容标签页并更容易分享它们，每个内容标签页会自动添加一个锚链接，您可以通过右键点击或在新标签页中打开：

=== "在新标签页中打开我 ..."

=== "... 或我 ..."

=== "... 或甚至我"

您可以复制标签的链接并在同一页面或任何其他页面创建链接。例如，您可以[跳转到上面这段文字的第三个标签][tab_1]或到[发布指南的Insiders][tab_2]。

!!! tip "可读的锚链接"

    [Python Markdown 扩展包] 9.6 添加了对内容标签页的[slugification]支持，生成更漂亮且更易读的锚链接。启用 slugify 功能，请添加以下行：

    ``` yaml
    markdown_extensions:
      - pymdownx.tabbed:
          slugify: !!python/object/apply:pymdownx.slugs.slugify
            kwds:
              case: lower
    ```

    有关更多信息，请[查看扩展指南][slugification]。

  [tab_1]: #anchor-links--or-even-me
  [tab_2]: ../publishing-your-site.md#with-github-actions-insiders
  [Python Markdown 扩展包]: https://facelessuser.github.io/pymdown-extensions/
  [slugification]: ../setup/extensions/python-markdown-extensions.md#+pymdownx.tabbed.slugify

### 关联内容标签页 {#linked-content-tabs}

<!-- md:version 8.3.0 -->
<!-- md:feature -->

启用后，整个文档站点的所有内容标签页将被关联，并在用户点击某个标签时切换到相同的标签。将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - content.tabs.link
```

内容标签页是基于它们的标签而不是位置关联的。这意味着当用户点击一个内容标签页时，所有具有相同标签的标签页都将被激活，不论它们在容器中的顺序如何。此外，此功能与[即时加载]完全集成，并在页面加载中持久存在。

=== "功能启用"

    [![Linked content tabs enabled]][Linked content tabs enabled]

=== "功能禁用"

    [![Linked content tabs disabled]][Linked content tabs disabled]

  [即时加载]: ../setup/setting-up-navigation.md#instant-loading
  [Linked content tabs enabled]: ../assets/screenshots/content-tabs-link.png
  [Linked content tabs disabled]: ../assets/screenshots/content-tabs.png

## 用法 {#usage}

### 分组代码块 {#grouping-code-blocks}

代码块是分组的主要目标之一，可以视为内容标签页的一个特例，因为带有单个代码块的标签页总是呈现时没有水平间距：

``` title="Content tabs with code blocks"
=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```
```

<div class="result" markdown>

=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```

</div>

### 分组其他内容 {#grouping-other-content}

当内容标签页包含多于一个代码块时，它会呈现出水平间距。永远不会添加垂直间距，但可以通过在其他块中嵌套标签页来实现：

``` title="Content tabs"
=== "Unordered list"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "Ordered list"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci
```

<div class="result" markdown>

=== "无序列表"

    * Sed sagittis eleifend rutrum
    * Donec vitae suscipit est
    * Nulla tempor lobortis orci

=== "有序列表"

    1. Sed sagittis eleifend rutrum
    2. Donec vitae suscipit est
    3. Nulla tempor lobortis orci

</div>

### 嵌入内容 {#embedded-content}

当启用 [SuperFences] 时，内容标签页可以包含任意嵌套内容，包括进一步的内容标签页，并可以嵌套在其他块中，如[警告]或引用：

``` title="Content tabs in admonition"
!!! example

    === "Unordered List"

        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```

    === "Ordered List"

        ``` markdown
        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci
        ```
```

<div class="result" markdown>

!!! example

    === "无序列表"

        ``` markdown
        * Sed sagittis eleifend rutrum
        * Donec vitae suscipit est
        * Nulla tempor lobortis orci
        ```

    === "有序列表"

        ``` markdown
        1. Sed sagittis eleifend rutrum
        2. Donec vitae suscipit est
        3. Nulla tempor lobortis orci
        ```

</div>

  [警告]: admonitions.md
