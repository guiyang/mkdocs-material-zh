---
icon: material/image-sync-outline
---

# 图像处理 {#image-processing}

一些[内置插件]依赖外部库进行高效的图像处理，尤其是[social]插件生成[社交卡片]，以及[optimize]插件应用[图像优化]。本指南说明如何在不同环境中安装这些库。

  [内置插件]: ../index.md
  [social]: ../social.md
  [社交卡片]: ../../setup/setting-up-social-cards.md
  [optimize]: ../optimize.md
  [图像优化]: ../../setup/building-an-optimized-site.md

## 依赖项 {#dependencies}

图像处理库是完全可选的，仅在您想使用[social]插件或[optimize]插件时需要安装。这些库在`imaging`附加组件下列出：

```
pip install "mkdocs-material[imaging]"
```

这将安装以下包的兼容版本：

- [Pillow]
- [CairoSVG]

  [Pillow]: https://pillow.readthedocs.io/
  [CairoSVG]: https://cairosvg.org/

### Cairo 图形库 {#cairo-graphics}

[Cairo Graphics]是一个图形库，也是[Pillow]的依赖项，Material for MkDocs 使用它来生成[社交卡片]和执行[图像优化]。以下部分解释了如何在您的系统上安装[Cairo Graphics]及其依赖项：

=== ":material-apple: macOS"

    确保安装了[Homebrew]，这是macOS的现代包管理器。接下来，使用以下命令安装所有必要的依赖项：

    ```
    brew install cairo freetype libffi libjpeg libpng zlib
    ```

=== ":fontawesome-brands-windows: Windows"

    如[安装指南]中所述，在Windows上安装[Cairo Graphics]库的最简单方法是安装[GTK+]。您还可以下载预编译的[GTK运行时]。

=== ":material-linux: Linux"

    Linux有多种包管理器，其可用性因发行版而异。[安装指南]解释了如何为您的发行版安装[Cairo Graphics]库：

    === ":material-ubuntu: Ubuntu"

        ```
        apt-get install libcairo2-dev libfreetype6-dev libffi-dev libjpeg-dev libpng-dev libz-dev
        ```

    === ":material-fedora: Fedora"

        ```
        yum install cairo-devel freetype-devel libffi-devel libjpeg-devel libpng-devel zlib-devel
        ```

    === ":fontawesome-brands-suse: openSUSE"

        ```
        zypper install cairo-devel freetype-devel libffi-devel libjpeg-devel libpng-devel zlib-devel
        ```

以下环境预安装了[Cairo Graphics]：

- [x] 在[Docker镜像]中无需安装
- [x] 在[GitHub Actions]（Ubuntu）中无需安装

  [Cairo Graphics]: https://www.cairographics.org/
  [Homebrew]: https://brew.sh/
  [安装指南]: https://www.cairographics.org/download/
  [GTK+]: https://www.gtk.org/docs/installations/windows/
  [GTK运行时]: https://github.com/tschoonj/GTK-for-Windows-Runtime-Environment-Installer/releases
  [Docker镜像]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [GitHub Actions]: ../../publishing-your-site.md#with-github-actions

### pngquant

[pngquant]是一个出色的用于有损PNG压缩的库，是[内置优化插件]的直接依赖项。以下部分解释了如何安装[pngquant]系统：

=== ":material-apple: macOS"

    确保安装了[Homebrew]，这是macOS的现代包管理器。接下来，使用以下命令安装所有必要的依赖项：

    ```
    brew install pngquant
    ```

=== ":fontawesome-brands-windows: Windows"

    在Windows上安装[pngquant]稍微复杂一些。[pngquant-winbuild]仓库包含了如何在Windows上设置[pngquant]环境的指南。

=== ":material-linux: Linux"

    所有流行的Linux发行版，无论包管理器如何，都应该允许使用捆绑的包管理器安装[pngquant]。例如，在Ubuntu上，可以使用以下命令安装[pngquant]：

    ```
    apt-get install pngquant
    ```

    对于 `yum` 和 `zypper` 也是如此。

以下环境预安装了[pngquant]：

- [x] 在[Docker镜像]中无需安装

  [pngquant]: https://pngquant.org/
  [built-in optimize plugin]: ../../plugins/optimize.md
  [pngquant-winbuild]: https://github.com/jibsen/pngquant-winbuild

### 故障排除 {#troubleshooting}

### 找不到Cairo库 {#cairo-library-was-not-found}

按照上面的安装指南操作后，您可能仍然遇到以下错误：

```bash
no library called "cairo-2" was found
no library called "cairo" was found
no library called "libcairo-2" was found
cannot load library 'libcairo.so.2': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.so.2'
cannot load library 'libcairo.2.dylib': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo.2.dylib'
cannot load library 'libcairo-2.dll': error 0x7e.  Additionally, ctypes.util.find_library() did not manage to locate a library called 'libcairo-2.dll'
```

这意味着安装了[`cairosvg`][PyPi CairoSVG]包，但底层的[`cairocffi`][PyPi CairoCFFI]依赖项无法[找到][cffi-dopen]已安装的库。根据操作系统，库查找过程有所不同：

!!! tip
    在继续之前，请记住完全重启所有打开的终端窗口及其父主机，如IDE，以重新加载在安装过程中更改的任何环境变量。这可能是快速解决方案。

=== ":material-apple: macOS"

    在macOS上，库查找会检查[dyld][osx-dyld]中定义的路径。此外，每个库`name`都会以[三种变体][find-library-macOS]检查，格式为`libname.dylib`、`name.dylib`和`name.framework/name`。

    [Homebrew]应该设置所有需要的变量指向已安装库的目录，但如果没有发生，您可以使用下面的调试脚本查看查找的路径。

    一个[已知的解决方法][cffi-issue]是在运行MkDocs之前直接添加Homebrew lib路径：

    ```bash
    export DYLD_FALLBACK_LIBRARY_PATH=/opt/homebrew/lib
    ```

    查看[cairo-lookup-macos.py]的源代码

    ```bash title="Python Debug macOS Script"
    curl "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-macos.py" | python -
    ```

=== ":fontawesome-brands-windows: Windows"

    在Windows上，库查找会检查环境`PATH`变量中定义的路径。此外，每个库`name`都会以[两种变体][find-library-Windows]检查，格式为`name`和`name.dll`。

    [GTK运行时]的默认安装路径为：

    ```powershell
    C:\Program Files\GTK3-Runtime Win64
    ```

    并且库在`<INSTALL-DIR>\lib`目录中。使用下面的调试脚本检查是否包含该路径。如果没有包含：

    1. 按++windows+r++。
    2. 运行`SystemPropertiesAdvanced`小程序。
    3. 在底部选择“环境变量”。
    4. 将整个路径添加到`lib`目录到您的`Path`变量中。
    5. 点击所有打开窗口的确定以应用更改。
    6. 完全重启任何打开的终端窗口及其父主机，如IDE。

    ```powershell title="You can also list paths using PowerShell"
    $env:Path -split ';'
    ```

    查看[cairo-lookup-windows.py]的源代码

    ```powershell title="PowerShell - Python Debug Windows Script"
    (Invoke-WebRequest "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-windows.py").Content | python -
    ```

=== ":material-linux: Linux"

    在Linux上，库查找[可能有很大差异][find-library-Linux]，这取决于已安装的发行版。对于经过测试的Ubuntu和Manjaro系统，Python运行shell命令来检查[`ldconfig`][ubuntu-ldconfig]、[`gcc`][ubuntu-gcc]/`cc`编译器以及[`ld`][ubuntu-ld]中有哪些库可用。

    您可以使用绝对路径扩展`LD_LIBRARY_PATH`环境变量，该路径指向包含`libcairo.so`等库的库目录。在运行MkDocs之前直接运行此命令：

    ```bash
    export LD_LIBRARY_PATH=/absolute/path/to/lib:$LD_LIBRARY_PATH
    ```

    您还可以修改`/etc/ld.so.conf`文件。

    下面的Python脚本显示了查找已安装库时运行的函数。您可以检查源代码以了解在库查找期间在您的系统上执行的具体命令。

    查看[cairo-lookup-linux.py]的源代码

    ```bash title="Python Debug Linux Script"
    curl "https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-linux.py" | python -
    ```

  [PyPi CairoSVG]: https://pypi.org/project/CairoSVG
  [PyPi CairoCFFI]: https://pypi.org/project/CairoCFFI
  [osx-dyld]: https://www.unix.com/man-page/osx/1/dyld/
  [ubuntu-ldconfig]: https://manpages.ubuntu.com/manpages/focal/en/man8/ldconfig.8.html
  [ubuntu-ld]: https://manpages.ubuntu.com/manpages/xenial/man1/ld.1.html
  [ubuntu-gcc]: https://manpages.ubuntu.com/manpages/trusty/man1/gcc.1.html
  [cffi-issue]: https://github.com/squidfunk/mkdocs-material/issues/5121
  [cffi-dopen]: https://github.com/Kozea/cairocffi/blob/f1984d644bbc462ef0ec33b97782cf05733d7b53/cairocffi/__init__.py#L24-L49
  [find-library-macOS]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L70-L81
  [find-library-Windows]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L59-L67
  [find-library-Linux]: https://github.com/python/cpython/blob/4d58a1d8fb27048c11bcbda3da1bebf78f979335/Lib/ctypes/util.py#L92
  [cairo-lookup-macos.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-macos.py
  [cairo-lookup-windows.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-windows.py
  [cairo-lookup-linux.py]: https://raw.githubusercontent.com/squidfunk/mkdocs-material/master/includes/debug/cairo-lookup-linux.py
