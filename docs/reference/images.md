---
icon: material/image-frame
---

# 图像 Images {#images}

尽管图像是 Markdown 的一等公民，并且是核心语法的一部分，但处理图像可能会有些困难。MkDocs 的 Material 工具使得处理图像更加舒适，提供了图像对齐和图像标题的样式。

## 配置 {#configuration}

此配置增加了对齐图像、添加图像标题（将其渲染为图表）和标记大图像以进行懒加载的能力。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - attr_list
  - md_in_html
```

查看更多配置选项：

- [属性列表]
- [HTML 中的 Markdown]

  [属性列表]: ../setup/extensions/python-markdown.md#attribute-lists
  [HTML 中的 Markdown]: ../setup/extensions/python-markdown.md#markdown-in-html

### Lightbox

<!-- md:version 0.1.0 -->
<!-- md:plugin [glightbox] -->

如果你想为你的文档添加图像缩放功能，[glightbox] 插件是一个绝佳的选择，因为它与 MkDocs 的 Material 完美集成。使用 `pip` 安装它：

```
pip install mkdocs-glightbox
```

然后，将以下行添加到 `mkdocs.yml`：

``` yaml
plugins:
  - glightbox
```

W我们建议查看可用的 [配置选项][glightbox options]。

  [glightbox]: https://github.com/blueswen/mkdocs-glightbox
  [glightbox options]: https://github.com/blueswen/mkdocs-glightbox#usage

## 使用 {#usage}

### 图像对齐 {#image-alignment}

当启用 [属性列表] 时，可以通过添加相应的对齐方向属性 `align`，即 `align=left` 或 `align=right`，来对齐图像：

=== "左对齐"

    ``` markdown title="Image, aligned to left"
    ![Image title](https://dummyimage.com/600x400/eee/aaa){ align=left }
    ```

    <div class="result" markdown>

    ![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=left width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

=== "右对齐"

    ``` markdown title="Image, aligned to right"
    ![Image title](https://dummyimage.com/600x400/eee/aaa){ align=right }
    ```

    <div class="result" markdown>

    ![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–){ align=right width=300 }

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

    </div>

如果没有足够的空间在图像旁边渲染文本，图像将扩展到视口的全宽，例如在移动视口上。

??? question "为什么没有居中对齐？"

    [`align`][align] 属性不允许居中对齐，这是为什么这个选项不被 MkDocs 的 Material 支持。[^1] 相反，可以使用 [图像标题] 语法，因为标题是可选的。

  [^1]:
    你也可能意识到 [`align`][align] 属性自 HTML5 起已被弃用，那为什么还要使用它呢？主要原因是可移植性——它仍然得到所有浏览器和客户端的支持，并且极不可能被完全移除，因为许多较旧的网站仍在使用它。这确保了在 Material for MkDocs 生成的网站之外查看 Markdown 文件时具有一致的外观。

  [align]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#deprecated_attributes
  [image captions]: #image-captions

### 图像标题 {#image-captions}

遗憾的是，Markdown 语法不提供对图像标题的原生支持，但始终可以使用 [HTML 中的 Markdown] 扩展与字面 `figure` 和 `figcaption` 标签一起使用：

``` html title="Image with caption"
<figure markdown="span">
  ![Image title](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>
```

<div class="result">
  <figure>
    <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
    <figcaption>Image caption</figcaption>
  </figure>
</div>

### 图像懒加载 {#image-lazy-loading}

现代浏览器通过 `loading=lazy` 指令提供了对图像懒加载的 [原生支持][lazy-loading]，在不支持的浏览器中会退化为急切加载：

``` markdown title="Image, lazy-loaded"
![Image title](https://dummyimage.com/600x400/){ loading=lazy }
```

<div class="result" markdown>
  <img src="https://dummyimage.com/600x400/f5f5f5/aaaaaa?text=–%20Image%20–" width="300" />
</div>

  [lazy-loading]: https://caniuse.com/#feat=loading-lazy-attr

### 浅色和深色模式 {#light-and-dark-mode}

<!-- md:version 8.1.1 -->

如果你添加了 [颜色调板切换] 并且想为浅色和深色配色方案显示不同的图像，你可以在图像 URL 中添加 `#only-light` 或 `#only-dark` 哈希片段：

``` markdown title="Image, different for light and dark mode"
![Image title](https://dummyimage.com/600x400/f5f5f5/aaaaaa#only-light)
![Image title](https://dummyimage.com/600x400/21222c/d5d7e2#only-dark)
```

<div class="result" markdown>

![Zelda light world]{ width="300" }
![Zelda dark world]{ width="300" }

</div>

!!! warning "使用 [自定义配色方案] 时的要求"

    内置的 [配色方案] 定义了上述哈希片段，但如果你使用 [自定义配色方案]，你还必须根据它是浅色方案还是深色方案，添加以下选择器：

    === "自定义浅色方案"

        ``` css
        [data-md-color-scheme="custom-light"] img[src$="#only-dark"],
        [data-md-color-scheme="custom-light"] img[src$="#gh-dark-mode-only"] {
          display: none; /* Hide dark images in light mode */
        }
        ```

    === "自定义深色方案"

        ``` css
        [data-md-color-scheme="custom-dark"] img[src$="#only-light"],
        [data-md-color-scheme="custom-dark"] img[src$="#gh-light-mode-only"] {
          display: none; /* Hide light images in dark mode */
        }
        ```

    请记得将 `#!css "custom-light"` 和 `#!css "custom-dark"` 更改为你的方案名称。

  [颜色调板切换]: ../setup/changing-the-colors.md#color-palette-toggle
  [Zelda light world]: ../assets/images/zelda-light-world.png#only-light
  [Zelda dark world]: ../assets/images/zelda-dark-world.png#only-dark
  [color schemes]: ../setup/changing-the-colors.md#color-scheme
  [custom color schemes]: ../setup/changing-the-colors.md#custom-color-schemes
