---
title: Getting started with Insiders
---

# 开始使用 Insiders {getting-started-with-insiders}

MkDocs 的 Material Insiders 是 MkDocs 的 Material 的兼容替代品，可以通过 [`pip`][pip]、[`docker`][docker] 或 [`git`][git] 类似的方式安装。请注意，要访问 Insiders 仓库，你需要成为 GitHub 上 @squidfunk 的[合格赞助商][become an eligible sponsor]。

  [pip]: #with-pip
  [docker]: #with-docker
  [git]: #with-git
  [become an eligible sponsor]: index.md#how-to-become-a-sponsor

## 要求 {#requirements}

在你被添加到协作者列表并接受仓库邀请后，下一步是为你的 GitHub 账户创建[个人访问令牌][personal access token]，以便从命令行或 GitHub Actions 工作流程中以编程方式访问 Insiders 仓库：

1.  访问 https://github.com/settings/tokens
2.  点击 [生成新令牌][Generate a new token]
3.  输入名称并选择 [`repo`][scopes] 范围
4.  生成令牌并将其安全存储

  [personal access token]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [Generate a new token]: https://github.com/settings/tokens/new
  [scopes]: https://docs.github.com/en/developers/apps/scopes-for-oauth-apps#available-scopes

下面的一些说明要求将 `GH_TOKEN` 环境变量设置为你在上一步生成的个人访问令牌的值。注意，个人访问令牌必须始终保密，因为它允许拥有者访问你的私人仓库。

## 安装 {#installation}

### 使用 pip {#with-pip}

可以使用 `pip` 安装 MkDocs 的 Material Insiders。通常，你会希望安装最新版本，但也可以安装特定的旧版本甚至最新的开发版本。确保按照上述指导设置了 `GH_TOKEN` 变量。

=== "特定版本"

    从 Insiders 仓库的[标签列表]中选择相应的标签。在下面的 `pip` 命令中，用你想要的标签替换 URL 末尾的标签。

    ``` sh
    pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git@9.4.2-insiders-4.42.0
    ```

=== "最新版本"

    ``` sh
    pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
    ```

[标签列表]: https://github.com/squidfunk/mkdocs-material-insiders/tags

### 使用 docker {#with-docker}

如果你想在 Docker 中使用 MkDocs 的 Material Insiders，需要一些额外的步骤。虽然我们不能为 Insiders 提供托管的 Docker 镜像[^2]，[GitHub 容器注册表]允许简单且舒适的自我托管：

1.  [Fork Insiders 仓库]
2.  在你的 fork 上启用 [GitHub Actions][^3]
3.  创建一个新的个人访问令牌[^4]
    1.  访问 https://github.com/settings/tokens
    2.  点击 [生成新令牌][Generate a new token]
    3.  输入名称并选择 [`write:packages`][scopes] 范围
    4.  生成令牌并将其安全存储
4.  在你的 fork 上添加 [GitHub Actions 秘密][GitHub Actions secret]
    1.  将名称设置为 `GHCR_TOKEN`
    2.  将值设置为在上一步中创建的个人访问令牌
5.  [创建新发布][Create a new release] 以构建和发布 Docker 镜像
6.  在你的 fork 上安装 [Pull App] 以保持与上游同步

当创建新的标签（发布）时，[`publish`][publish] 工作流[^5]会自动运行。当上游仓库发布新的 Insiders 版本时，[Pull App] 会创建一个带有更改的拉取请求，并拉入新的标签，该标签由 [`publish`][publish] 工作流自动构建并发布到你的私有注册表。

现在，你应该能够从你的私有注册表拉取 Docker 镜像：

```
docker login -u ${GH_USERNAME} -p ${GHCR_TOKEN} ghcr.io
docker pull ghcr.io/${GH_USERNAME}/mkdocs-material-insiders
```

如果你希望在 insiders 容器镜像中添加额外的插件，请按照[入门指南](../getting-started.md#with-docker)中概述的步骤操作。

  [^2]:
    之前，Insiders 提供了一个专门的 Docker 镜像，可供所有赞助商使用。2021年3月21日，由于在 #2442 中概述和讨论的原因，该镜像被弃用。它于2021年6月1日被移除。

  [^3]:
    当你 fork 一个仓库时，GitHub 会禁用所有工作流。虽然这是一个合理的默认设置，但你需要启用 GitHub Actions 才能自动构建并发布 Docker 镜像到 [GitHub 容器注册表]。

  [^4]:
    虽然你可以只为访问 Insiders 仓库创建的个人访问令牌添加 `write:packages` 范围，但为了安全起见，最好创建一个专用令牌，你只用它来发布 Docker 镜像。

  [^5]:
    Insiders 仓库包含两个 GitHub Actions 工作流：

    - `build.yml` – 构建和检查项目（在 forks 上禁用）
    - `publish.yml` – 构建和发布 Docker 镜像

### 使用 git {#with-git}

当然，你也可以直接通过 `git` 使用 MkDocs 的 Material Insiders：

```
git clone git@github.com:squidfunk/mkdocs-material-insiders.git mkdocs-material
```

主题将位于 `mkdocs-material/material` 文件夹中。当从 `git` 克隆时，必须安装主题，以便 MkDocs 能找到内置插件：

```
pip install -e mkdocs-material
```

  [GitHub 容器注册表]: https://docs.github.com/en/packages/guides/about-github-container-registry
  [Fork Insiders 仓库]: https://github.com/squidfunk/mkdocs-material-insiders/fork
  [GitHub Actions]: https://docs.github.com/en/github/administering-a-repository/disabling-or-limiting-github-actions-for-a-repository
  [packages scope]: https://docs.github.com/en/developers/apps/scopes-for-oauth-apps#available-scopes
  [GitHub Actions secret]: https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository
  [Create a new release]: https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository#creating-a-release
  [Pull App]: https://github.com/apps/pull
  [publish]: https://github.com/squidfunk/mkdocs-material-insiders/blob/master/.github/workflows/publish.yml

## 内置插件 {#built-in-plugins}

当你使用仅通过 Insiders 提供的内置插件时，外部贡献者将无法在他们的本地机器上构建你的文档项目。这就是为什么我们开发了[内置组插件][built-in group plugin]，它允许有条件地加载插件：

``` yaml
plugins:
  - search
  - social

  # CI=1 mkdocs build
  - group:
      enabled: !ENV CI
      plugins:
        - git-revision-date-localized
        - git-committers

  # INSIDERS=1 mkdocs build
  - group:
      enabled: !ENV INSIDERS
      plugins:
        - optimize
        - privacy
```

当然，你也可以启用两个组：

```
CI=1 INSIDERS=1 mkdocs build
```

  [^1]:
    以前我们推荐使用[配置继承][configuration inheritance]来解决这些限制，但全新的[内置组插件][built-in group plugin]是一个更好的方法，因为它允许你使用单一的配置文件来构建你的项目，无论是使用社区版还是 Insiders 版本的 MkDocs 的 Material。

  [built-in group plugin]: ../plugins/group.md
  [configuration inheritance]: https://www.mkdocs.org/user-guide/configuration/#configuration-inheritance
