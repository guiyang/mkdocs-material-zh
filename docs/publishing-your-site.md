# 发布站点 {#publishing-your-site}

在 `git` 仓库中托管项目文档的一个优点是，当推送新更改时能够自动部署它。MkDocs 使这变得非常简单。

## GitHub 页面 {#github-pages}

如果您已在 GitHub 上托管您的代码，[GitHub 页面]无疑是发布项目文档的最便捷方式。它免费且设置相当简单。

  [GitHub 页面]: https://pages.github.com/

### 使用 GitHub Actions {#with-gitHub-actions}

使用 [GitHub Actions]，您可以自动化项目文档的部署。在仓库的根目录下，创建一个新的 GitHub Actions 工作流，例如 `.github/workflows/ci.yml`，并复制粘贴以下内容：

=== "Material for MkDocs"

    ``` yaml
    name: ci # (1)!
    on:
      push:
        branches:
          - master # (2)!
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v4
          - name: Configure Git Credentials
            run: |
              git config user.name github-actions[bot]
              git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          - uses: actions/setup-python@v5
            with:
              python-version: 3.x
          - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV # (3)!
          - uses: actions/cache@v4
            with:
              key: mkdocs-material-${{ env.cache_id }}
              path: .cache
              restore-keys: |
                mkdocs-material-
          - run: pip install mkdocs-material # (4)!
          - run: mkdocs gh-deploy --force
    ```

    1.  您可以根据喜好更改 name 名称。

    2.  在某个时点，GitHub 将 `master` 重命名为 `main`。如果您的默认分支命名为 `master`，您可以安全地删除 `main`，反之亦然。

    3.  存储 `cache_id` 环境变量，以便稍后在创建缓存 `key` 时访问它。名称区分大小写，因此请确保与 `${{ env.cache_id }}` 一致。

        - `--utc` 选项确保每个工作流运行器使用相同的时区。
        - `%V` 格式保证每周更新一次缓存。
        - 您可以将格式更改为 `%F` 以进行每日缓存更新。

        您可以阅读 [手册页面] 以了解更多关于 `date` 命令的格式化选项。

    4.  这是安装更多 [MkDocs 插件] 或在构建过程中使用的 Markdown 扩展的地方：

        ``` sh
        pip install \
          mkdocs-material \
          mkdocs-awesome-pages-plugin \
          ...
        ```

=== "Insiders"

    ``` yaml
    name: ci
    on:
      push:
        branches:
          - master
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        if: github.event.repository.fork == false
        steps:
          - uses: actions/checkout@v4
          - name: Configure Git Credentials
            run: |
              git config user.name github-actions[bot]
              git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          - uses: actions/setup-python@v5
            with:
              python-version: 3.x
          - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
          - uses: actions/cache@v4
            with:
              key: mkdocs-material-${{ env.cache_id }}
              path: .cache
              restore-keys: |
                mkdocs-material-
          - run: apt-get install pngquant # (1)!
          - run: pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
          - run: mkdocs gh-deploy --force
    env:
      GH_TOKEN: ${{ secrets.GH_TOKEN }} # (2)!
    ```

    1.  如果您想使用 [内置优化插件] 自动压缩图像，此步骤是必需的。

    2.  部署 [Insiders] 时，请记得将 `GH_TOKEN` 环境变量设置为您的 [个人访问令牌] 的值，这可以通过 [GitHub secrets] 完成。

现在，当新提交被推送到 `master` 或 `main` 分支时，静态站点会自动构建并部署。推送您的更改以查看工作流程是否有效。

如果几分钟后 GitHub 页面没有显示，请转到您的仓库设置，并确保您的 GitHub 页面的 [发布源分支] 设置为 `gh-pages`。

您的文档很快就会出现在 `<username>.github.io/<repository>` 上。

  [GitHub Actions]: https://github.com/features/actions
  [MkDocs 插件]: https://github.com/mkdocs/mkdocs/wiki/MkDocs-Plugins
  [个人访问令牌]: https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token
  [Insiders]: insiders/index.md
  [内置优化插件]: plugins/optimize.md
  [GitHub secrets]: https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
  [发布源分支]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
  [手册页面]: https://man7.org/linux/man-pages/man1/date.1.html

### 使用 MkDocs {#with-mkdocs}

如果您更喜欢手动部署项目文档，可以从包含 `mkdocs.yml` 文件的目录中调用以下命令：

```
mkdocs gh-deploy --force
```

这将构建您的文档并将其部署到仓库中的 `gh-pages` 分支。有关更多信息，请查看 [MkDocs 问当中的概述部分]。有关参数的描述，请查看 [命令说明文档]。

  [MkDocs 问当中的概述部分]: https://www.mkdocs.org/user-guide/deploying-your-docs/#project-pages
  [命令说明文档]: https://www.mkdocs.org/user-guide/cli/#mkdocs-gh-deploy

## GitLab 页面 {#gitlab-pages}

如果您在 GitLab 上托管代码，可以通过使用 [GitLab CI] 任务运行器来部署到 [GitLab 页面]。在仓库的根目录下创建一个名为 `.gitlab-ci.yml` 的任务定义，并复制粘贴以下内容：

=== "Material for MkDocs"

    ``` yaml
    pages:
      stage: deploy
      image: python:latest
      script:
        - pip install mkdocs-material
        - mkdocs build --site-dir public
      artifacts:
        paths:
          - public
      rules:
        - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
    ```

=== "Insiders"

    ``` yaml
    pages:
      stage: deploy
      image: python:latest
      script: # (1)!
        - pip install git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
        - mkdocs build --site-dir public
      artifacts:
        paths:
          - public
      rules:
        - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
    ```

    1.  部署 [Insiders] 时，请记得将 `GH_TOKEN` 环境变量设置为您的 [个人访问令牌] 的值，这可以通过 [遮蔽的自定义变量] 完成。

现在，当新提交被推送到 [默认分支]（通常为 `master` 或 `main`）时，静态站点会自动构建并部署。提交并推送文件到您的仓库以查看工作流程是否有效。

您的文档很快就会出现在 `<username>.gitlab.io/<repository>` 上。

## 其他 {#other}

由于我们无法涵盖所有可能的平台，我们依赖社区贡献的指南来解释如何将使用 Material for MkDocs 构建的网站部署到其他提供商：

<div class="mdx-columns" markdown>

- [:simple-azuredevops: Azure][Azure]
- [:simple-cloudflarepages: Cloudflare Pages][Cloudflare Pages]
- [:simple-digitalocean: DigitalOcean][DigitalOcean]
- [:material-airballoon-outline: Fly.io][Flyio]
- [:simple-netlify: Netlify][Netlify]
- [:simple-vercel: Vercel][Vercel]
- [:simple-codeberg: Codeberg Pages][Codeberg Pages]

</div>

  [GitLab 页面]: https://gitlab.com/pages
  [GitLab CI]: https://docs.gitlab.com/ee/ci/
  [遮蔽的自定义变量]: https://docs.gitlab.com/ee/ci/variables/#create-a-custom-variable-in-the-ui
  [默认分支]: https://docs.gitlab.com/ee/user/project/repository/branches/default.html
  [Azure]: https://bawmedical.co.uk/t/publishing-a-material-for-mkdocs-site-to-azure-with-automatic-branch-pr-preview-deployments/763
  [Cloudflare Pages]: https://www.starfallprojects.co.uk/projects/deploy-host-docs/deploy-mkdocs-material-cloudflare/
  [DigitalOcean]: https://www.starfallprojects.co.uk/projects/deploy-host-docs/deploy-mkdocs-material-digitalocean-app-platform/
  [Flyio]: https://documentation.breadnet.co.uk/cloud/fly/mkdocs-on-fly/
  [Netlify]: https://www.starfallprojects.co.uk/projects/deploy-host-docs/deploy-mkdocs-material-netlify/
  [Vercel]: https://www.starfallprojects.co.uk/projects/deploy-host-docs/deploy-mkdocs-material-vercel/
  [Codeberg Pages]: https://andre601.ch/blog/2023/11-05-using-codeberg-pages/
