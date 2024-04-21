---
icon: material/button-cursor
---

# 按钮 Button {#buttons}

Material for MkDocs 为主要和次要按钮提供了专门的样式，可以添加到任何链接、`label` 或 `button` 元素上。这对于有专门 _呼叫操作_ 的文档或登陆页面特别有用。

## 配置 {#configuration}

此配置允许为所有内联和块级元素添加属性，通过简单的语法将任何链接转换成按钮。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
```

查看其他配置选项：

- [属性列表]

  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists

## 用法 {#usage}

### 添加按钮 {#adding-buttons}

为了将链接渲染为按钮，请在其后加上花括号并添加 `.md-button` 类选择器。按钮将接收选定的[主颜色]和[强调色]（如果激活）。

``` markdown title="Button"
[Subscribe to our newsletter](#){ .md-button }
```

<div class="result" markdown>

[Subscribe to our newsletter][演示]{ .md-button }

</div>

  [主颜色]: ../setup/changing-the-colors.md#primary-color
  [强调色]: ../setup/changing-the-colors.md#accent-color
  [演示]: javascript:alert$.next("Demo")

### 添加主要按钮 {#adding-primary-buttons}

如果您想显示一个填充的主要按钮（如 Material for MkDocs 的[首页]上），请添加 `.md-button` 和 `.md-button--primary` CSS 类选择器。

``` markdown title="Button, primary"
[Subscribe to our newsletter](#){ .md-button .md-button--primary }
```

<div class="result" markdown>

[Subscribe to our newsletter][演示]{ .md-button .md-button--primary }

</div>

  [landing page]: ../index.md

### 添加图标按钮 {#adding-icon-buttons}

当然，可以通过使用[图标语法]和任何有效的图标简码（可以通过我们的[图标搜索]轻松找到）向所有类型的按钮添加图标。

``` markdown title="Button with icon"
[Send :fontawesome-solid-paper-plane:](#){ .md-button }
```

<div class="result" markdown>

[Send :fontawesome-solid-paper-plane:][演示]{ .md-button }

</div>

  [图标语法]: icons-emojis.md#using-icons
  [图标搜索]: icons-emojis.md#search
