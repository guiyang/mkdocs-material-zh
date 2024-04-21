# 入门 {#getting-started}

Material for MkDocs 是一个基于 [MkDocs] 的强大文档框架，MkDocs 是一个用于项目文档的静态网站生成器。[^1] 如果您熟悉Python，可以通过 [`pip`][pip]，Python的包管理器，来安装 Material for MkDocs。如果不熟悉，我们推荐使用 [`docker`][docker]。


  [^1]:
      Material for MkDocs 最初于2016年作为 MkDocs 的一个简单主题开始，但在几年的发展中，它已经远超过原有的设计 -- 通过众多内置插件、设置以及无数的自定义功能，Material for MkDocs 现在已经成为创建项目文档最简单、最强大的框架之一。

  [MkDocs]: https://www.mkdocs.org
  [pip]: #with-pip
  [docker]: #with-docker

## 安装 {#installation}

### 使用 pip <small>推荐</small> {#with-pip}

Material for MkDocs 已发布为 [Python 包] 并且可以通过 `pip` 安装，理想情况下通过使用 [虚拟环境]。打开终端并安装 Material for MkDocs：

=== "Latest"

    ``` sh
    pip install mkdocs-material
    ```

=== "9.x"

    ``` sh
    pip install mkdocs-material=="9.*" # (1)!
    ```

    1.  Material for MkDocs 使用 [语义化版本控制][^2]，这就是为什么限制升级到当前主要版本的好处。

        这将确保您不会意外 [升级到下一个主要版本]，可能包括不会提示的破坏性更改，从而影响您的站点。此外，您可以使用 `pip freeze` 创建一个锁定文件，以使构建在任何时候都可重现：

        ```
        pip freeze > requirements.txt
        ```

        现在，可以使用 lockfile 件进行安装：

        ```
        pip install -r requirements.txt
        ```

  [^2]:
    请注意，有时现有功能的改进会作为补丁版本发布，例如改进内容标签的渲染，因为它们不被视为新功能。

这将自动安装所有兼容版本的依赖项：[MkDocs]、[Markdown]、[Pygments] 和 [Python Markdown Extensions]。Material for MkDocs 一直努力支持最新版本，因此无需单独安装这些包。

---

:fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__[如何设置 Material for MkDocs]__ 作者 @james-willett – :octicons-clock-24:
15分钟 – 了解如何使用 Material for MkDocs 在 GitHub Pages 上创建和托管文档站点的指南。

  [如何设置 Material for MkDocs]: https://www.youtube.com/watch?v=Q-YA_dA8C20

---

!!! tip

    如果您没有 Python 的使用经验，我们建议阅读[使用 Python 的 pip 来管理项目依赖]，这是关于 Python 包管理机制的很好的介绍，并且可以帮助您解决遇到的错误。

  [Python 包]: https://pypi.org/project/mkdocs-material/
  [虚拟环境]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment
  [语义化版本控制]: https://semver.org/
  [升级到下一个主要版本]: upgrade.md
  [Markdown]: https://python-markdown.github.io/
  [Pygments]: https://pygments.org/
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [使用 Python 的 pip 来管理项目依赖]: https://realpython.com/what-is-pip/

### 使用 docker {#with-docker}

官方 [Docker 镜像] 是快速启动和运行的好方法，因为它已预装所有依赖。打开终端并拉取镜像：

=== "Latest"

    ```
    docker pull squidfunk/mkdocs-material
    ```

=== "9.x"

    ```
    docker pull squidfunk/mkdocs-material:9
    ```

`mkdocs` 可执行文件作为入口点提供，`serve` 是默认命令。如果您不熟悉 Docker，请不必担心，我们将在接下来的部分为您提供帮助。

以下插件与 Docker 镜像一同捆绑：

- [mkdocs-minify-plugin]
- [mkdocs-redirects]

  [Docker 镜像]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [mkdocs-minify-plugin]: https://github.com/byrnereese/mkdocs-minify-plugin
  [mkdocs-redirects]: https://github.com/datarobot/mkdocs-redirects

??? question "如何向 Docker 镜像添加插件？"

    Material for MkDocs 只捆绑选择的插件，以保持官方镜像的体积小。如果您想使用的插件未包括在内，您可以轻松添加它们：

    === "Material for MkDocs"

        创建一个 `Dockerfile` 并扩展官方镜像：

        ``` Dockerfile title="Dockerfile"
        FROM squidfunk/mkdocs-material
        RUN pip install mkdocs-macros-plugin
        RUN pip install mkdocs-glightbox
        ```

    === "Insiders"

        克隆或分叉 Insiders 仓库，并在仓库根目录创建一个名为 `user-requirements.txt` 的文件。然后，向文件中添加应安装的插件，例如：

        ``` txt title="user-requirements.txt"
        mkdocs-macros-plugin
        mkdocs-glightbox
        ```

    接下来，使用以下命令构建镜像：

    ```
    docker build -t squidfunk/mkdocs-material .
    ```

    新镜像将安装额外的包，并且可以像使用官方镜像一样使用。

### 使用 git {#with-git}

Material for MkDocs 可以直接从 [GitHub] 通过克隆到您的项目根目录下的子文件夹中使用，这可能有助于您使用最新版本：

```
git clone https://github.com/squidfunk/mkdocs-material.git
```

接下来，安装主题及其依赖：

```
pip install -e mkdocs-material
```

  [GitHub]: https://github.com/squidfunk/mkdocs-material
