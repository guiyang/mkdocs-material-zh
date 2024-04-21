---
icon: material/format-list-bulleted
---

# 列表 Lists {#lists}

MkDocs 的 Material 支持多种列表风格，以适应不同的使用场景，包括 _无序列表_ 和 _有序列表_，这些都通过标准 Markdown 支持，以及 _定义列表_ 和 _任务列表_，这些则通过扩展支持。

## 配置 {#configuration}

此配置启用了定义列表和任务列表的使用，这两者都不是标准 Markdown 语法的一部分。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - def_list
  - pymdownx.tasklist:
      custom_checkbox: true
```

查看更多配置选项：

- [定义列表]
- [任务列表]

  [定义列表]: ../setup/extensions/python-markdown.md#definition-lists
  [任务列表]: ../setup/extensions/python-markdown-extensions.md#tasklist

## 使用 {#usage}

### 使用无序列表 {#using-unordered-lists}

无序列表可以通过在行前加上 `-`、`*` 或 `+` 列表标记来编写，这些标记可以互换使用。此外，所有类型的列表都可以互相嵌套：

``` markdown title="List, unordered"
- Nulla et rhoncus turpis. Mauris ultricies elementum leo. Duis efficitur
  accumsan nibh eu mattis. Vivamus tempus velit eros, porttitor placerat nibh
  lacinia sed. Aenean in finibus diam.

    * Duis mollis est eget nibh volutpat, fermentum aliquet dui mollis.
    * Nam vulputate tincidunt fringilla.
    * Nullam dignissim ultrices urna non auctor.
```

<div class="result" markdown>

- Nulla et rhoncus turpis. Mauris ultricies elementum leo. Duis efficitur
  accumsan nibh eu mattis. Vivamus tempus velit eros, porttitor placerat nibh
  lacinia sed. Aenean in finibus diam.

    * Duis mollis est eget nibh volutpat, fermentum aliquet dui mollis.
    * Nam vulputate tincidunt fringilla.
    * Nullam dignissim ultrices urna non auctor.

</div>

### 使用有序列表 {#using-ordered-lists}

有序列表必须以数字开头，后跟一个点。数字不需要连续，可以都设置为 `1.`，因为它们会在渲染时重新编号：

``` markdown title="List, ordered"
1.  Vivamus id mi enim. Integer id turpis sapien. Ut condimentum lobortis
    sagittis. Aliquam purus tellus, faucibus eget urna at, iaculis venenatis
    nulla. Vivamus a pharetra leo.

    1.  Vivamus venenatis porttitor tortor sit amet rutrum. Pellentesque aliquet
        quam enim, eu volutpat urna rutrum a. Nam vehicula nunc mauris, a
        ultricies libero efficitur sed.

    2.  Morbi eget dapibus felis. Vivamus venenatis porttitor tortor sit amet
        rutrum. Pellentesque aliquet quam enim, eu volutpat urna rutrum a.

        1.  Mauris dictum mi lacus
        2.  Ut sit amet placerat ante
        3.  Suspendisse ac eros arcu
```

<div class="result" markdown>

1.  Vivamus id mi enim. Integer id turpis sapien. Ut condimentum lobortis
    sagittis. Aliquam purus tellus, faucibus eget urna at, iaculis venenatis
    nulla. Vivamus a pharetra leo.

    1.  Vivamus venenatis porttitor tortor sit amet rutrum. Pellentesque aliquet
        quam enim, eu volutpat urna rutrum a. Nam vehicula nunc mauris, a
        ultricies libero efficitur sed.

    2.  Morbi eget dapibus felis. Vivamus venenatis porttitor tortor sit amet
        rutrum. Pellentesque aliquet quam enim, eu volutpat urna rutrum a.

        1.  Mauris dictum mi lacus
        2.  Ut sit amet placerat ante
        3.  Suspendisse ac eros arcu

</div>

### 使用定义列表 {#using-definition-lists}

启用 [定义列表] 后，可以使用简单的语法列举函数或模块的任意键值对参数：

``` markdown title="Definition list"
`Lorem ipsum dolor sit amet`

:   Sed sagittis eleifend rutrum. Donec vitae suscipit est. Nullam tempus
    tellus non sem sollicitudin, quis rutrum leo facilisis.

`Cras arcu libero`

:   Aliquam metus eros, pretium sed nulla venenatis, faucibus auctor ex. Proin
    ut eros sed sapien ullamcorper consequat. Nunc ligula ante.

    Duis mollis est eget nibh volutpat, fermentum aliquet dui mollis.
    Nam vulputate tincidunt fringilla.
    Nullam dignissim ultrices urna non auctor.
```

<div class="result" markdown>

`Lorem ipsum dolor sit amet`

:   Sed sagittis eleifend rutrum. Donec vitae suscipit est. Nullam tempus
    tellus non sem sollicitudin, quis rutrum leo facilisis.

`Cras arcu libero`

:   Aliquam metus eros, pretium sed nulla venenatis, faucibus auctor ex. Proin
    ut eros sed sapien ullamcorper consequat. Nunc ligula ante.

    Duis mollis est eget nibh volutpat, fermentum aliquet dui mollis.
    Nam vulputate tincidunt fringilla.
    Nullam dignissim ultrices urna non auctor.

</div>

### 使用任务列表 {#using-task-lists}

启用 [任务列表] 后，无序列表项可以前缀 `[ ]` 以呈现未选中的复选框，或 `[x]` 以呈现选中的复选框，从而定义任务列表：

``` markdown title="Task list"
- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    * [x] In hac habitasse platea dictumst
    * [x] In scelerisque nibh non dolor mollis congue sed et metus
    * [ ] Praesent sed risus massa
- [ ] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque
```

<div class="result" markdown>

- [x] Lorem ipsum dolor sit amet, consectetur adipiscing elit
- [ ] Vestibulum convallis sit amet nisi a tincidunt
    * [x] In hac habitasse platea dictumst
    * [x] In scelerisque nibh non dolor mollis congue sed et metus
    * [ ] Praesent sed risus massa
- [ ] Aenean pretium efficitur erat, donec pharetra, ligula non scelerisque

</div>
