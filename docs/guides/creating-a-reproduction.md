# 创建复现步骤 {#creating-a-reproduction}

复现步骤是指重现软件中某个特定错误的简化版过程。它包括所有必要的最小设置和说明，并且应尽可能简单，同时能够展示问题所在。

## 指南 {#guide}

### 环境 <small>可选</small> { #environment }

我们推荐使用[虚拟环境][virtual environment]，这是一个隔离的Python运行时环境。如果你在虚拟环境中，你安装或升级的任何包都只限于该环境中。如果遇到问题，你可以简单地删除并重建环境。设置非常简单：

-   创建一个新的虚拟环境：

    ```
    python3 -m venv venv
    ```

-   激活环境：

    === ":material-apple: macOS"

        ``` sh
        . venv/bin/activate
        ```

    === ":fontawesome-brands-windows: Windows"

        ``` sh
        . venv/Scripts/activate
        ```

    === ":material-linux: Linux"

        ``` sh
        . venv/bin/activate
        ```


    此时你的终端应该在提示符前显示`(venv)`，这表示你已经处于刚刚创建的虚拟环境中。

-   退出环境：

    ```
    deactivate
    ```

  [virtual environment]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment

### 最小化复现 {#minimal-reproduction}

按照下面的说明，你将设置一个项目骨架来创建复现。如上所述，我们推荐使用[虚拟环境][virtual environment]，因此在你的工作目录中创建一个新文件夹，并在其中设置一个新的虚拟环境。接下来：

1.  正如我们在[错误报告指南][bug reporting guide]中提到的，确保你运行的是Material for MkDocs的最新版本，这可能已经包含了对该错误的修复：

    ```
    pip install --upgrade --force-reinstall mkdocs-material
    ```

2.  使用`mkdocs`可执行文件启动一个新的文档项目，作为复现的基础。创建一个全新的空项目至关重要：

    ```
    mkdocs new .
    ```

    首先在`mkdocs.yml`中添加[最小配置][minimal configuration]：

    ``` yaml
    theme:
      name: material
    ```

3.  现在，只在`mkdocs.yml`中添加必要的设置以保持复现的最小化。如果你正在为渲染错误创建复现，只创建必要的Markdown文档。__重复此步骤直到你想报告的错误能够被观察到。__

4.  在将所有内容打包进一个`.zip`文件之前的最后一步，再次检查所有设置和文件是否必要，这意味着如果省略它们错误就不会发生。移除所有非必要的行和文件。

  [bug reporting guide]: ../contributing/reporting-a-bug.md#upgrade-to-latest-version
  [minimal configuration]: ../creating-your-site.md#minimal-configuration

### 创建 `.zip` 文件 {#creating-a-zip-file}

Material for MkDocs 9.0.0包括一个新插件，专门用于为错误报告创建复现。当启用内置的信息插件时，MkDocs会将所有相关文件添加到一个`.zip`中，打印摘要到终端并退出。在`mkdocs.yml`中添加以下行：

``` yaml
plugins:
  - info
```

现在，当运行`mkdocs build`时，一个名为`example.zip`的文件会自动创建，包含你可以直接附加到你的错误报告中的最小复现。

```
INFO     -  Started archive creation for bug report
INFO     -  Archive successfully created:

  example/.dependencies.json 859.0 B
  example/.versions.log 83.0 B
  example/docs/index.md 282.0 B
  example/mkdocs.yml 56.0 B

  example.zip 1.8 kB
```
