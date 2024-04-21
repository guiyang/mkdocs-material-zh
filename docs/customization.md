# 自定义 {#customization}

项目文档多样化，正如项目本身一样，而 Material for MkDocs 是使其美观的绝佳起点。然而，在编写文档时，您可能会达到需要进行小的调整以保持品牌风格的时刻。

## 添加资源 {#adding-assets}

[MkDocs] 提供了几种自定义主题的方式。为了对 Material for MkDocs 进行一些小的调整，您可以在 `docs` 目录中添加 CSS 和 JavaScript 文件。

  [MkDocs]: https://www.mkdocs.org

### 额外的 CSS {#additional-css}

如果您想调整一些颜色或改变某些元素的间距，可以在一个单独的样式表中进行。最简单的方法是在 `docs` 目录中创建一个新的样式表文件：

``` { .sh .no-copy }
.
├─ docs/
│  └─ stylesheets/
│     └─ extra.css
└─ mkdocs.yml
```

然后，将以下行添加到 `mkdocs.yml` 中：

``` yaml
extra_css:
  - stylesheets/extra.css
```

### 额外的 JavaScript {#additional-javaScrip}

如果您想集成另一个语法高亮显示器或向主题添加一些自定义逻辑，请在 `docs` 目录中创建一个新的 JavaScript 文件：

``` { .sh .no-copy }
.
├─ docs/
│  └─ javascripts/
│     └─ extra.js
└─ mkdocs.yml
```

然后，将以下行添加到 `mkdocs.yml` 中：

``` yaml
extra_javascript:
  - javascripts/extra.js
```

??? tip "如何与第三方 JavaScript 库集成"

    您可能希望在浏览器完全加载页面后才运行您的 JavaScript 代码。这意味着安装一个回调函数订阅 Material for MkDocs 导出的 `document$` 可观察对象的事件。使用 `document$` 可观察对象尤其重要，如果您使用 [即时加载]，因为它不会在浏览器中刷新页面 - 但订阅者会被通知。

    ``` javascript
    document$.subscribe(function() {
      console.log("Initialize third-party libraries here")
    })
    ```

    `document$` 是一个 [RxJS 可观察对象]，您可以多次调用 `subscribe()` 方法以附加不同的功能。

  [即时加载]: setup/setting-up-navigation.md/#instant-loading
  [RxJS 可观察对象]: https://rxjs.dev/api/index/class/Observable

## 扩展主题 {#extending-the-theme}

如果您想改变 HTML 源代码（例如添加或删除某些部分），您可以扩展主题。MkDocs 支持 [主题扩展]，这是一个简单的方法，可以覆盖 Material for MkDocs 的部分内容而无需从 git 分叉。这确保您可以更容易地更新到最新版本。

  [主题扩展]: https://www.mkdocs.org/user-guide/customizing-your-theme/#using-the-theme-custom_dir

### 设置和主题结构 {#setup-and-theme-structure}

像往常一样在 `mkdocs.yml` 中启用 Material for MkDocs，并为 `overrides` 创建一个新文件夹，然后使用 [`custom_dir`][custom_dir] 设置引用它：

``` yaml
theme:
  name: material
  custom_dir: overrides
```

!!! warning "主题扩展的先决条件"

    由于 [`custom_dir`][custom_dir] 设置用于主题扩展过程，因此需要通过 `pip` 安装 Material for MkDocs 并在 `mkdocs.yml` 中用 [`name`][name] 设置引用它。当从 `git` 克隆时，这不会起作用。

`overrides` 目录中的结构必须镜像原始主题的目录结构，因为 `overrides` 目录中的任何文件都将替换原始主题中同名的文件。此外，更多资产也可以放在 `overrides` 目录中：

``` { .sh .no-copy }
.
├─ .icons/                             # 绑定的图标集
├─ assets/
│  ├─ images/                          # 图片和图标
│  ├─ javascripts/                     # JavaScript 文件
│  └─ stylesheets/                     # 样式表
├─ partials/
│  ├─ integrations/                    # 第三方集成
│  │  ├─ analytics/                    # 分析集成
│  │  └─ analytics.html                # 分析设置
│  ├─ languages/                       # 翻译语言
│  ├─ actions.html                     # 操作
│  ├─ alternate.html                   # 站点语言选择器
│  ├─ comments.html                    # 评论系统（默认为空）
│  ├─ consent.html                     # 同意
│  ├─ content.html                     # 页面内容
│  ├─ copyright.html                   # 版权和主题信息
│  ├─ feedback.html                    # 这个页面有帮助吗？
│  ├─ footer.html                      # 底部栏
│  ├─ header.html                      # 顶部栏
│  ├─ icons.html                       # 自定义图标
│  ├─ language.html                    # 翻译设置
│  ├─ logo.html                        # 页眉和侧边栏的 Logo
│  ├─ nav.html                         # 主导航
│  ├─ nav-item.html                    # 主导航项
│  ├─ pagination.html                  # 分页（用于博客）
│  ├─ palette.html                     # 颜色调板切换
│  ├─ post.html                        # 博客文章摘要
│  ├─ progress.html                    # 进度指示器
│  ├─ search.html                      # 搜索界面
│  ├─ social.html                      # 社交链接
│  ├─ source.html                      # 仓库信息
│  ├─ source-file.html                 # 源文件信息
│  ├─ tabs.html                        # 标签导航
│  ├─ tabs-item.html                   # 标签导航项
│  ├─ tags.html                        # 标签
│  ├─ toc.html                         # 目录
│  ├─ toc-item.html                    # 目录项
│  └─ top.html                         # 返回顶部按钮
├─ 404.html                            # 404 错误页面
├─ base.html                           # 基础模板
├─ blog.html                           # 博客索引页面
├─ blog-archive.html                   # 博客归档索引页面
├─ blog-category.html                  # 博客类别索引页面
├─ blog-post.html                      # 博客文章页面
└─ main.html                           # 默认页面
```

  [custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [name]: https://www.mkdocs.org/user-guide/configuration/#name

### 覆盖 {#overriding-partials}

为了覆盖一个部分，我们可以用 `overrides` 目录中同名和位置的文件替换它。例如，要替换原始的 `footer.html` 部分，请在 `overrides` 目录中创建一个新的 `footer.html` 部分：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ partials/
│     └─ footer.html
└─ mkdocs.yml
```

MkDocs 现在将在渲染主题时使用新的部分。这可以对任何文件进行。

### 覆盖块 <small>recommended</small> {#overriding-blocks}

除了覆盖部分外，也可以覆盖（并扩展）模板块，这些块在模板内部定义并包围特定功能。为了设置块覆盖，请在 `overrides` 目录中创建一个 `main.html` 文件：

``` { .sh .no-copy }
.
├─ overrides/
│  └─ main.html
└─ mkdocs.yml
```

然后，例如要覆盖站点标题，请在 `main.html` 中添加以下行：

``` html
{% extends "base.html" %}

{% block htmltitle %}
  <title>Lorem ipsum dolor sit amet</title>
{% endblock %}
```

如果您打算 __add__ 某些内容到块中而不是完全用新内容替换它，请在块中使用 `{{ super() }}` 以包含原始块内容。这在添加第三方脚本到您的文档中时特别有用，例如。


``` html
{% extends "base.html" %}

{% block scripts %}
  <!-- Add scripts that need to run before here -->
  {{ super() }}
  <!-- Add scripts that need to run afterwards here -->
{% endblock %}
```

主题提供以下模板块：

| 块名称             | 用途                                            |
| :---------------- | :---------------------------------------------- |
| `analytics`       | 包含 Google Analytics 集成                        |
| `announce`        | 包含公告栏                                        |
| `config`          | 包含 JavaScript 应用配置                          |
| `container`       | 包含主内容容器                                    |
| `content`         | 包含主内容                                        |
| `extrahead`       | 空块，用于添加自定义 meta 标签                     |
| `fonts`           | 包含字体定义                                      |
| `footer`          | 包含带导航和版权信息的页脚                          |
| `header`          | 包含固定头部栏                                    |
| `hero`            | 包含英雄宣传片（如果可用）                          |
| `htmltitle`       | 包含 `<title>` 标签                               |
| `libs`            | 包含 JavaScript 库（头部）                         |
| `outdated`        | 包含版本警告                                      |
| `scripts`         | 包含 JavaScript 应用（页脚）                        |
| `site_meta`       | 包含文档头部的 meta 标签                           |
| `site_nav`        | 包含站点导航和目录表                              |
| `styles`          | 包含样式表（也包括额外来源）                        |
| `tabs`            | 包含标签导航（如果可用）                            |


## 主题开发

Material for MkDocs 是在 [TypeScript]、[RxJS] 和 [SASS] 之上构建的，并使用一个精简的自定义构建过程将一切整合在一起。[^1] 如果您想进行更根本的更改，可能需要直接在主题的源码中进行调整并重新编译它。

  [^1]:
    在 <!-- md:version 7.0.0 --> 之前，构建基于 Webpack，由于与加载器和插件的不兼容，偶尔会导致构建失败。因此，我们决定用基于 [RxJS] 的更精简的解决方案替换 Webpack，这也是应用本身的基础。这使得我们能够减少超过 500 个依赖（约减少 30%）。

  [TypeScript]: https://www.typescriptlang.org/
  [RxJS]: https://github.com/ReactiveX/rxjs
  [SASS]: https://sass-lang.com

### 环境设置 {#environment-setup}

首先，克隆您想要工作的版本的仓库。如果您想克隆 [Insiders] 仓库，您需要先成为赞助商以获得访问权限。

  [Insiders]: insiders/index.md

=== "Material for MkDocs"

    ```
    git clone https://github.com/squidfunk/mkdocs-material
    cd mkdocs-material
    ```

=== "Insiders"

    您需要拥有一个 GitHub 访问令牌 [如 Insiders 文档中所述] 并在 `$GH_TOKEN` 变量中使其可用。

    ``` sh
    git clone https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git # (1)!
    ```

    1.  If you are using SSH keys for authenticating with GitHub, you can
        clone Insiders with this command:

        ```
        git clone git@github.com:squidfunk/mkdocs-material-insiders.git
        ```

    [如 Insiders 文档中所述]: insiders/getting-started.md#requirements

接下来，创建一个新的 [Python 虚拟环境][venv] 并 [激活][venv-activate] 它：

```
python -m venv venv
source venv/bin/activate
```

!!! note "确保 pip 始终在虚拟环境中运行"

    如果您将环境变量 `PIP_REQUIRE_VIRTUALENV` 设置为 `true`，`pip` 将拒绝在虚拟环境之外安装任何东西。忘记激活 `venv` 非常烦人，因为它会随着时间的推移在虚拟环境之外安装各种东西，可能导致进一步的错误。因此，您可能希望将此添加到您的 `.bashrc` 或 `.zshrc` 中，并重启您的 shell：

    ```
    export PIP_REQUIRE_VIRTUALENV=true
    ```

  [venv]: https://docs.python.org/3/library/venv.html
  [venv-activate]: https://docs.python.org/3/library/venv.html#how-venvs-work

然后，安装所有 Python 依赖项：

=== "Material for MkDocs"

    ```
    pip install -e ".[recommended]"
    pip install nodeenv
    ```

=== "Insiders"

    ```
    pip install -e ".[recommended, imaging]"
    pip install nodeenv
    ```

    此外，您还需要根据 [图像处理] 要求指南在系统中安装 `cairo` 和 `pngquant` 库。

    [图像处理]: plugins/requirements/image-processing.md


最后，在 Python 虚拟环境中安装 [Node.js] LTS 版本并安装所有 Node.js 依赖项：

```
nodeenv -p -n lts
npm install
```

  [Node.js]: https://nodejs.org

### 开发模式 {#development-mode}

启动观察者：

```
npm start
```

然后，在第二个终端窗口中启动 MkDocs 实时预览服务器：

```
mkdocs serve --watch-theme
```

将浏览器指向 [localhost:8000][live preview]，您应该会看到这份文档。

!!! warning "自动生成的文件"

    切勿更改 `material` 目录中的任何内容，因为该目录的内容是从 `src` 目录自动生成的，并且在构建主题时会被覆盖。

  [live preview]: http://localhost:8000

### 构建主题 {#building-the-theme}

完成更改后，您可以通过调用以下命令构建主题：

``` sh
npm run build # (1)!
```

1.  虽然此命令将构建所有主题文件，但它将跳过用于 Material for MkDocs 自己文档的覆盖，这些覆盖不会与主题一起分发。如果您分叉了主题并希望同时构建覆盖，例如在提交更改的 PR 之前，请使用：

    ```
    npm run build:all
    ```

    这将花费更长时间，因为现在将构建图标搜索索引、模式文件以及额外的样式表和 JavaScript 文件。

这将触发所有样式表和 JavaScript 文件的生产级编译和缩小化。命令退出后，编译后的文件位于 `material` 目录中。运行 `mkdocs build` 时，您应该能看到对原始主题的更改。
