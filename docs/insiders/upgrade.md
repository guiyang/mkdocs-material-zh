# 如何升级

在升级 Insiders 时，你应始终检查构成版本限定符第一部分的 MkDocs 的 Material 版本，例如，Insiders `4.x.x` 当前基于 `9.x.x`：

```
9.x.x-insiders-4.x.x
```

如果主版本号增加，最好查阅[升级指南][upgrade guide]并遵循其中的步骤，以确保你的配置是最新的，并且已经进行了所有必要的更改。

  [upgrade guide]: ../upgrade.md
  [list of tags]: https://github.com/squidfunk/mkdocs-material-insiders/tags

根据你的安装方式以及你想升级到的版本，你需要运行不同的命令：

=== "通过 pip 升级到发布版本"

    如果你是通过 `pip` 安装 Insiders 并且想升级到特定发布版本，从[标签列表][list of tags]中选取标签，并在下面命令的 URL 末尾替换该标签：

    ```
    pip install --upgrade git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git@9.4.2-insiders-4.42.0
    ```

=== "通过 pip 升级到最新开发版本"

    如果你是通过 `pip` 安装 Insiders 并且想升级到最新的开发版本，运行：

    ```
    pip install --upgrade git+https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git
    ```

=== "通过 git 升级"

    如果你是通过 `git` 安装 Insiders，你首先需要检出你想安装的版本到你的工作空间。完成这一步后，你可以运行 `pip` 来安装该版本。

    首先，确保你的本地克隆与上游仓库保持同步，运行 `git pull`。

    你可以使用 `git tag --sort -refname` 查看标签，或者参阅[标签列表][list of tags]。然后，用你想使用的标签替换下面命令中给出的标签（两次），并在你的工作空间运行它[^detached]:

      [^detached]:
        `--detach` 参数用于告诉 `git` 你同意将你的工作空间置于[分离头][detached head]状态，这在这里完全是可以接受的。

      [detached head]: https://www.git-tower.com/learn/git/faq/detached-head-when-checkout-commit/

    ```
    cd mkdocs-material
    git checkout --detach tags/9.4.2-insiders-4.42.0
    ```

    现在，回到你的 Git 仓库所在的父目录并运行 `pip`：

    ```
    cd ..
    pip install -e mkdocs-material
    ```


