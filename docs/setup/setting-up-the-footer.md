# 设置页脚 {#setting-up-the-footer}

您的项目文档的页脚是添加链接到您或您的公司正在使用的网站或平台的绝佳位置，作为额外的营销渠道，例如 :fontawesome-brands-mastodon:{ style="color: #5A4CE0" } 或 :fontawesome-brands-youtube:{ style="color: #EE0F0F" }，您可以通过 `mkdocs.yml` 轻松配置这些。

## 配置 {#configuration}

### 导航 {#navigation}

<!-- md:version 9.0.0 -->
<!-- md:feature -->

页脚可以包含指向当前页面的前一页和后一页的链接。如果您希望启用此行为，请将以下行添加到 `mkdocs.yml`：

``` yaml
theme:
  features:
    - navigation.footer
```

### 社交链接 {#social-links}

<!-- md:version 1.0.0 -->
<!-- md:default none -->

社交链接作为页脚的一部分显示在版权声明旁边。在 `mkdocs.yml` 中添加一系列社交链接：

``` yaml
extra:
  social:
    - icon: fontawesome/brands/mastodon # (1)!
      link: https://fosstodon.org/@squidfunk
```

1.  输入一些关键字使用我们的[图标搜索]找到完美的图标，并点击短代码将其复制到剪贴板：

    <div class="mdx-iconsearch" data-mdx-component="iconsearch">
      <input class="md-input md-input--stretch mdx-iconsearch__input" placeholder="Search icon" data-mdx-component="iconsearch-query" value="mastodon" />
      <div class="mdx-iconsearch-result" data-mdx-component="iconsearch-result" data-mdx-mode="file">
        <div class="mdx-iconsearch-result__meta"></div>
        <ol class="mdx-iconsearch-result__list"></ol>
      </div>
    </div>

以下属性可用于每个链接：

<!-- md:option social.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须包含有效的图标路径，该路径包含在主题中，否则构建将不会成功。一些流行的选择包括：

    * :fontawesome-brands-github: – `fontawesome/brands/github`
    * :fontawesome-brands-gitlab: – `fontawesome/brands/gitlab`
    * :fontawesome-brands-x-twitter: – `fontawesome/brands/x-twitter`
    * :fontawesome-brands-mastodon: – `fontawesome/brands/mastodon`
      <small>automatically adds [`rel=me`][rel=me]</small>
    * :fontawesome-brands-docker: – `fontawesome/brands/docker`
    * :fontawesome-brands-facebook: – `fontawesome/brands/facebook`
    * :fontawesome-brands-instagram: – `fontawesome/brands/instagram`
    * :fontawesome-brands-linkedin: – `fontawesome/brands/linkedin`
    * :fontawesome-brands-slack: – `fontawesome/brands/slack`
    * :fontawesome-brands-discord: – `fontawesome/brands/discord`
    * :fontawesome-brands-pied-piper-alt: – `fontawesome/brands/pied-piper-alt`

<!-- md:option social.link -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须设置为相对或绝对 URL，包括 URI 方案。所有 URI 方案都受支持，包括 `mailto` 和 `bitcoin`：

    === ":fontawesome-brands-mastodon: Mastodon"

        ``` yaml
        extra:
          social:
            - icon: fontawesome/brands/mastodon
              link: https://fosstodon.org/@squidfunk
        ```

    === ":octicons-mail-16: Email"

        ``` yaml
        extra:
          social:
            - icon: fontawesome/solid/paper-plane
              link: mailto:<email-address>
        ```

<!-- md:option social.name -->

:   <!-- md:default _domain name from_ `link`_, if available_ -->
    此属性用作链接的 `title` 属性，可以设置为可识别的名称以提高可访问性：

    ``` yaml
    extra:
      social:
        - icon: fontawesome/brands/mastodon
          link: https://fosstodon.org/@squidfunk
          name: squidfunk on Fosstodon
    ```

  [图标搜索]: ../reference/icons-emojis.md#search
  [rel=me]: https://docs.joinmastodon.org/user/profile/#verification

### 版权声明 {#copyright-notice}

<!-- md:version 0.1.0 -->
<!-- md:default none -->

作为页脚的一部分，可以渲染自定义的版权横幅，它显示在社交链接旁边。它可以作为 `mkdocs.yml` 的一部分定义：

``` yaml
copyright: Copyright &copy; 2016 - 2020 Martin Donath
```

### 生成器声明 {#generator-notice}

<!-- md:version 7.3.0 -->
<!-- md:default `true` -->

页脚显示 _由 Material for MkDocs 制作_ 的声明以表明网站是如何生成的。可以通过 `mkdocs.yml` 中的以下选项删除此声明：

``` yaml
extra:
  generator: false
```

!!! info "在删除生成器声明之前请阅读此信息"

    页脚中细微的 __由 Material for MkDocs 制作__ 提示是这个项目如此受欢迎的原因之一，因为它告诉用户网站是如何生成的，帮助新用户发现这个项目。在删除之前，请考虑您正在免费享受 @squidfunk 的工作成果，因为这个项目是开源的，并且拥有宽松的许可证。数千小时的工作投入到这个项目中，大部分时间没有任何经济回报。

    因此，如果您移除此声明，请考虑[赞助][Insiders]该项目。__谢谢您__ :octicons-heart-fill-24:{ .mdx-heart .mdx-insiders }

  [Insiders]: ../insiders/index.md

## 使用 {#usage}

### 隐藏前后链接 {#hiding-prev-next-links}

页脚导航显示指向前一页和后一页的链接，可以通过前置元素 `hide` 属性隐藏。在 Markdown 文件的顶部添加以下行：

``` yaml
---
hide:
  - footer
---

# Page title
...
```

## 自定义 {#customization}

### 自定义版权 {#custom-copyright}

<!-- md:version 8.0.0 -->
<!-- md:flag customization -->

为了自定义和覆盖[版权声明]，[扩展主题]并[覆盖 `copyright.html` 部分][overriding partials]，通常包括在 `mkdocs.yml` 中设置的 `copyright` 属性。

  [版权声明]: #copyright-notice
  [generator notice]: #generator-notice
  [扩展主题]: ../customization.md#extending-the-theme
  [overriding partials]: ../customization.md#overriding-partials
