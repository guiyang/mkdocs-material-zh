---
icon: material/alphabet-greek
---

# 数学 Math {#math}

[MathJax] 和 [KaTeX] 是两个流行的库，用于在浏览器中显示数学内容。虽然这两个库提供类似的功能，但它们使用不同的语法并拥有不同的配置选项。本文档网站提供了如何轻松地将它们与 MkDocs 的 Material 集成的信息。

  [MathJax]: https://www.mathjax.org/
  [LaTeX]: https://en.wikibooks.org/wiki/LaTeX/Mathematics
  [MathML]: https://en.wikipedia.org/wiki/MathML
  [AsciiMath]: http://asciimath.org/
  [KaTeX]: https://katex.org/

## 配置 {#configuration}

以下配置启用了使用 [MathJax] 和 [KaTeX] 渲染块和行内块方程的支持。

### MathJax

[MathJax] 是一个强大且灵活的库，支持多种输入格式，如 [LaTeX]、[MathML]、[AsciiMath]，以及各种输出格式，如 HTML、SVG、MathML。要在你的项目中使用 MathJax，请将以下行添加到你的 `mkdocs.yml`。

=== ":octicons-file-code-16: `docs/javascripts/mathjax.js`"

    ``` js
    window.MathJax = {
      tex: {
        inlineMath: [["\\(", "\\)"]],
        displayMath: [["\\[", "\\]"]],
        processEscapes: true,
        processEnvironments: true
      },
      options: {
        ignoreHtmlClass: ".*|",
        processHtmlClass: "arithmatex"
      }
    };

    document$.subscribe(() => { // (1)!
      MathJax.startup.output.clearCache()
      MathJax.typesetClear()
      MathJax.texReset()
      MathJax.typesetPromise()
    })
    ```

    1. 这将 MathJax 与 [即时加载] 集成。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.arithmatex:
          generic: true

    extra_javascript:
      - javascripts/mathjax.js
      - https://polyfill.io/v3/polyfill.min.js?features=es6
      - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
    ```

查看更多配置选项：

- [Arithmatex]

  [Arithmatex]: ../setup/extensions/python-markdown-extensions.md#arithmatex
  [即时加载]: ../setup/setting-up-navigation.md#instant-loading

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<script>
  window.MathJax = {
    tex: {
      inlineMath: [["\\(", "\\)"]],
      displayMath: [["\\[", "\\]"]],
      processEscapes: true,
      processEnvironments: true
    },
    options: {
      ignoreHtmlClass: ".*|",
      processHtmlClass: "arithmatex"
    }
  };
</script>

### KaTeX

[KaTeX] 是一个轻量级库，专注于速度和简洁。它支持 LaTeX 语法的子集，并且可以将数学内容渲染为 HTML 和 SVG。要在你的项目中使用 [KaTeX]，请将以下行添加到你的 `mkdocs.yml`。

=== ":octicons-file-code-16: `docs/javascripts/katex.js`"

    ``` js
    document$.subscribe(({ body }) => { // (1)!
      renderMathInElement(body, {
        delimiters: [
          { left: "$$",  right: "$$",  display: true },
          { left: "$",   right: "$",   display: false },
          { left: "\\(", right: "\\)", display: false },
          { left: "\\[", right: "\\]", display: true }
        ],
      })
    })
    ```

    1. 这将 KaTeX 与 [即时加载] 集成。

=== ":octicons-file-code-16: `mkdocs.yml`"

    ``` yaml
    markdown_extensions:
      - pymdownx.arithmatex:
          generic: true

    extra_javascript:
      - javascripts/katex.js
      - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.js
      - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/contrib/auto-render.min.js

    extra_css:
      - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.css
    ```

## 使用 {#usage}

### 使用块语法 {#using-block-syntax}

块必须用 `#!latex $$...$$` 或 `#!latex \[...\]` 分别封闭在独立行内：

``` latex title="block syntax"
$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$
```

<div class="result" markdown>

$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$

</div>

### 使用行内块语法 {#using-inline-block-syntax}

行内块必须用 `#!latex $...$` 或 `#!latex \(...\)` 封闭：

``` latex title="inline syntax"
The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.
```

<div class="result" markdown>

The homomorphism $f$ is injective if and only if its kernel is only the
singleton set $e_G$, because otherwise $\exists a,b\in G$ with $a\neq b$ such
that $f(a)=f(b)$.

</div>

## 比较 MathJax 和 KaTeX {#comparing-mathjax-and-kaTeX}

在决定使用 MathJax 还是 KaTeX 时，有几个关键因素需要考虑：

- __速度__：KaTeX 通常比 MathJax 更快。如果你的网站需要快速渲染大量复杂的方程式，KaTeX 可能是更好的选择。

- __语法支持__：MathJax 支持更广泛的 LaTeX 命令，并且可以处理多种数学标记语言（如 AsciiMath 和 MathML）。如果你需要高级 LaTeX 功能，MathJax 可能更适合。

- __输出格式__：两个库都支持 HTML 和 SVG 输出。然而，MathJax 还提供 MathML 输出，这对于可访问性至关重要，因为它可以被屏幕阅读器读取。

- __可配置性__：MathJax 提供了一系列配置选项，允许对其行为进行更精确的控制。如果你有特定的渲染要求，MathJax 可能是一个更灵活的选择。

- __浏览器支持__：虽然两个库在现代浏览器中都表现良好，但 MathJax 对较旧的浏览器具有更广泛的兼容性。如果你的观众使用各种浏览器，包括较旧的浏览器，MathJax 可能是一个更安全的选择。

总之，KaTeX 以其速度和简洁性脱颖而出，而 MathJax 则以提供更多功能和更好的兼容性为代价换取速度。在两者之间的选择将很大程度上取决于你的特定需求和限制。
