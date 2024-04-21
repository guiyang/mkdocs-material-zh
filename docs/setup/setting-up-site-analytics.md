# 设置站点分析 {#setting-up-site-analytics}

如同网络上提供的任何其他服务一样，了解您的项目文档实际使用情况可能是成功的关键因素。Material for MkDocs 与 [Google Analytics] 原生集成，并提供可定制的 [cookie 同意] 和 [反馈小部件]。

  [Google Analytics]: https://developers.google.com/analytics
  [cookie 同意]: ensuring-data-privacy.md#cookie-consent
  [反馈小部件]: #was-this-page-helpful

## 配置 {#configuration}

### Google Analytics

<!-- md:version 7.1.8 -->
<!-- md:default none -->

Material for MkDocs 与 Google Analytics 4[^1] 原生集成。如果您已经设置了 Google Analytics 并拥有一个属性，请通过添加以下行到 `mkdocs.yml` 来启用它：

  [^1]:
    在 Material for MkDocs 9.2.0 之前，也支持 Universal Analytics。但是，由于 Universal Analytics 已经停用，这一集成在 9.2.0 中被移除。

``` yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

??? question "如何测量站点搜索使用情况？"

    除了页面浏览和事件，[站点搜索]也可以被跟踪，以更好地了解人们如何使用您的文档以及他们期望找到什么。为了启用站点搜索跟踪，需要执行以下步骤：

    1. 转到您的 Google Analytics __管理设置__
    2. 选择相应跟踪代码的属性
    3. 选择 __数据流__ 标签并点击相应的 URL
    4. 在 __增强测量__ 部分点击齿轮图标
    5. 确保启用了 __站点搜索__

  [站点搜索]: setting-up-site-search.md

### 这个页面有帮助吗？ {#was-this-page-helpful}

<!-- md:version 8.4.0 -->
<!-- md:default none -->

在每个页面的底部可以包含一个简单的 [反馈小部件]，鼓励用户立即反馈页面是否有帮助。在 `mkdocs.yml` 中添加以下行：

``` yaml
extra:
  analytics: # (1)!
    feedback:
      title: Was this page helpful?
      ratings:
        - icon: material/emoticon-happy-outline
          name: This page was helpful
          data: 1
          note: >-
            Thanks for your feedback!
        - icon: material/emoticon-sad-outline
          name: This page could be improved
          data: 0
          note: >- # (2)!
            Thanks for your feedback! Help us improve this page by
            using our <a href="..." target="_blank" rel="noopener">feedback form</a>.
```

1.  这个功能与 [Google Analytics][analytics] 原生集成，这就是为什么也需要 `provider` 和 `property`。然而，也可以提供一个 [自定义反馈集成]。

2.  您可以向提交反馈后显示的注释中添加任意 HTML 标签，例如链接到反馈表单。

两个属性，`title` 和 `ratings`，是必需的。请注意，允许定义两个以上的评级，例如实施 1-5 星级评级。由于反馈小部件将数据发送到第三方服务，因此它当然与 [cookie 同意] 功能原生集成[^2]。

  [^2]:
    如果用户不接受 `analytics` cookie，反馈小部件将不会显示。

??? question "如何可视化收集的反馈评级？"

    要可视化反馈评级，您需要在 [Google Analytics] 中创建一个自定义报告，快速显示您的项目文档中评级最低和评级最高的页面。

    1.  转到您的 Google Analytics __仪表板__

    2.  在左侧菜单中转到 __配置__ 页面，然后选择 __自定义定义__

    3.  点击 __自定义指标__ 标签，然后 __创建自定义指标__，输入以下值：

        * Metric name (指标名称): Page helpful (页面有帮助)
        * Description (描述): Was this page helpful? (这个页面有帮助吗？)
        * Event parameter (事件参数): `data`
        * Unit of measurement (测量单位): Standard (标准)

    4.  在左侧菜单中转到 __探索__ 页面，创建一个新的 __空白探索__

    5.  配置报告如下：

        * Dimensions (维度): Add `Event name` and `Page location` (添加 `事件名称` 和 `页面位置`)
        * Metrics (指标): Add `Event count` and `Page helpful` (the custom metric created in step 3) (添加 `事件计数` 和 `页面有帮助`) (在步骤 3 中创建的自定义指标)
        * Rows (行): `Page location` (`页面位置`)
        * Values (值): Drag in both `Event count` and `Page helpful` (拖入 `事件计数` 和 `页面有帮助`)
        * Filters (过滤器): Add a new filter for `Event name / exactly matches / feedback` 添加一个新的过滤器 `事件名称 / 精确匹配 / 反馈`

    !!! warning "数据可用性延迟"

        报告可能需要 24 小时或更长时间才能开始显示数据

    现在，在您保存了报告并收集了一些反馈评级后，您将拥有一个页面列表，其中包含总评级数和每个页面的平均评级。这应该帮助您识别需要改进的页面：

    !!! danger "Google Analytics 4 不支持平均值"

        据我们所知，Google Analytics 4 目前没有功能允许定义一个自定义计算指标来计算页面的平均评级。请参见 #5740。

    [![feedback report]][feedback report]

每个评级的以下属性可用：

<!-- md:option analytics.feedback.ratings.icon -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性必须指向一个有效的图标路径，引用 [主题中捆绑的任何图标][custom icons]，否则构建将不会成功。一些流行的组合：

    * :material-emoticon-happy-outline: + :material-emoticon-sad-outline: – `material/emoticon-happy-outline` + `material/emoticon-sad-outline`
    * :material-thumb-up-outline: + :material-thumb-down-outline: – `material/thumb-up-outline` + `material/thumb-down-outline`
    * :material-heart: + :material-heart-broken: – `material/heart` + `material/heart-broken`

<!-- md:option analytics.feedback.ratings.name -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在用户交互时显示（即键盘焦点或鼠标悬停），解释图标背后的评级含义。

<!-- md:option analytics.feedback.ratings.data -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值将作为自定义事件的数据值发送到 Google Analytics[^3]（或任何自定义集成）。

  [^3]:
    请注意，对于 Google Analytics，数据值必须是整数。

<!-- md:option analytics.feedback.ratings.note -->

:   <!-- md:default none --> <!-- md:flag required -->
    此属性的值在用户选择评级后显示。它可以包含任意 HTML 标签，这对于要求用户通过表单为当前页面提供更详细的反馈非常有用。也可以使用以下占位符预填充表单：

    - `{url}` – 页面 URL
    - `{title}` – 页面标题

    ```
    https://github.com/.../issues/new/?title=[Feedback]+{title}+-+{url}
    ```

    在这个例子中，当点击链接时，用户将被重定向到您仓库的“新问题”表单，其中包括当前文档路径的预填充标题，例如：

    ```
    [Feedback] Setting up site analytics – /setup/setting-up-site-analytics/
    ```

    除 GitHub 问题外的另一种选择是 [Google 表单]。

  [feedback widget]: #feedback
  [analytics]: #google-analytics
  [feedback report]: ../assets/screenshots/feedback-report.png
  [自定义反馈集成]: #custom-site-feedback
  [custom icons]: https://github.com/squidfunk/mkdocs-material/tree/master/material/templates/.icons
  [Google 表单]: https://www.google.com/forms/about/

## 使用 {#usage}

### 隐藏反馈小部件 {#hiding-the-feedback-widget}

The [feedback widget] can be hidden for a document with the front matter `hide`
property. Add the following lines at the top of a Markdown file:
可以为带有前 matter `hide` 属性的文档隐藏 [反馈小部件]。在 Markdown 文件的顶部添加以下行：

``` yaml
---
hide:
  - feedback
---

# Page title
...
```

## 自定义 {#customization}

### 自定义站点分析 {#custom-site-analytics}

为了整合另一种提供基于 JavaScript 的跟踪解决方案的分析服务提供商，只需按照 [主题扩展] 指南操作，并在 `overrides` 文件夹中创建一个新的部分。该部分的名称用于通过 `mkdocs.yml` 配置自定义集成：

=== ":octicons-file-code-16: `overrides/partials/integrations/analytics/custom.html`"

    ``` html
    <script>
      /* Add custom analytics integration here, e.g. */
      var property = "{{ config.extra.analytics.property }}" // (1)!

      /* Wait for page to load and application to mount */
      document.addEventListener("DOMContentLoaded", function() {
        location$.subscribe(function(url) {
          /* Add custom page event tracking here */ // (2)!
        })
      })
    </script>
    ```

    1.  作为一个示例，此变量接收在 `mkdocs.yml` 中设置的值，对于 `property` 是 `"foobar"`。
    2.  如果您使用 [即时加载]，可以使用 `location$` 可观察对象来监听导航事件，它总是发出当前 `URL` 的信号。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra:
      analytics:
        provider: custom
        property: foobar # (1)!
    ```

    1.  您可以添加任意键值组合来配置您的自定义集成。如果您在多个存储库中共享自定义集成，这特别有用。

  [主题扩展]: ../customization.md#extending-the-theme
  [即时加载]: setting-up-navigation.md#instant-loading

### 自定义站点反馈 {#custom-site-feedback}

自定义反馈小部件集成只需要处理用户与反馈小部件互动生成的事件，这可以通过一些 [额外的 JavaScript] 来实现：

=== ":octicons-file-code-16: `docs/javascripts/feedback.js`"

    ``` js
    var feedback = document.forms.feedback
    feedback.hidden = false // (1)!

    feedback.addEventListener("submit", function(ev) {
      ev.preventDefault()

      var page = document.location.pathname // (2)!
      var data = ev.submitter.getAttribute("data-md-value")

      console.log(page, data) // (3)!

      feedback.firstElementChild.disabled = true // (4)!

      var note = feedback.querySelector(
        ".md-feedback__note [data-md-value='" + data + "']"
      )
      if (note)
        note.hidden = false // (5)!
    })
    ```

    1.  反馈小部件默认隐藏，因此在人们关闭 JavaScript 时不会显示。因此，需要在这里打开它。

    2.  检索页面和反馈值。

    3.  替换此代码以将数据发送到您的分析提供商。

    4.  提交后禁用表单。

    5.  显示配置的注释。显示哪一个取决于用户反馈。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    extra_javascript:
      - javascripts/feedback.js
    ```

&nbsp;
{ #feedback style="margin: 0; height: 0" }

  [额外的 JavaScript]: ../customization.md#additional-javascript
