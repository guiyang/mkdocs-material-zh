# 错误报告 {#bug-reports}

MkDocs 的 Material 是一个活跃维护的项目，我们始终致力于改进。对于这样一个庞大且复杂的项目，有时可能会出现错误。如果你认为你发现了一个错误，你可以通过在我们的公共[问题跟踪器][issue tracker]提交一个问题来帮助我们，按照本指南操作。

  [issue tracker]: https://github.com/squidfunk/mkdocs-material/issues

## 在创建问题之前 {#before-creating-an-issue}

这个项目拥有超过20,000名用户，每隔一天就会有问题被创建。这个项目的维护者们正在努力通过尽快修复错误来减少未解决问题的数量。按照本指南，你将清楚我们需要哪些信息来快速帮助你。

__但在创建问题之前，请先做以下几件事。__

### 升级到最新版本 {#upgrade-to-latest-version}

很有可能你发现的错误在后续版本中已经修复。因此，在报告问题之前，请确保你正在运行[MkDocs 的 Material 的最新版本][latest version]。请查阅我们的[升级指南][upgrade guide]了解如何升级到最新版本。

!!! warning "错误修复不会回溯到旧版本"

    请理解，只有在最新版本的 MkDocs 的 Material 中出现的错误才会被处理。此外，为了减少重复工作，修复不能回溯到早期版本。

### 移除自定义设置 {#remove-customizations}

如果你使用了[自定义设置][customizations]，如[额外的 CSS][additional CSS]、[JavaScript][JavaScript] 或[主题扩展][theme extension]，请在报告错误之前从 `mkdocs.yml` 中移除它们。我们无法为可能隐藏在你的自定义设置中的错误提供官方支持，因此请确保从 `mkdocs.yml` 中省略以下设置：

  - [`theme.custom_dir`][theme.custom_dir]
  - [`hooks`][hooks]
  - [`extra_css`][extra_css]
  - [`extra_javascript`][extra_javascript]

如果在移除这些设置后错误消失了，那么错误可能是由你的自定义设置引起的。一个好主意是逐步添加它们回去，以缩小问题的根源。如果你进行了重大版本升级，请确保你调整了所有你覆盖的部分。

!!! warning "我们文档中提到的自定义设置"

    MkDocs 的 Material 提供的一些功能只能通过自定义设置来实现。如果你在[我们的文档明确提到的自定义设置][that our documentation explicitly mentions]中发现了一个错误，我们当然鼓励你报告它。

__如果在解决问题时遇到困难，不要害羞，在我们的[讨论板][discussion board]上寻求帮助。__

  [latest version]: ../changelog/index.md
  [upgrade guide]: ../upgrade.md
  [Customizations]: ../customization.md
  [additional CSS]: ../customization.md#additional-css
  [JavaScript]: ../customization.md#additional-javascript
  [theme extension]: ../customization.md#extending-the-theme
  [theme.custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [hooks]: https://www.mkdocs.org/user-guide/configuration/#hooks
  [extra_css]: https://www.mkdocs.org/user-guide/configuration/#extra_css
  [extra_javascript]: https://www.mkdocs.org/user-guide/configuration/#extra_javascript
  [discussion board]: https://github.com/squidfunk/mkdocs-material/discussions
  [StackOverflow]: https://stackoverflow.com
  [that our documentation explicitly mentions]: ?q="extends+base"

### 寻找解决方案 {#search-for-solutions}

在这个阶段，我们知道问题在最新版本中依然存在，并且不是由你的任何自定义设置引起的。然而，问题可能是由于 `mkdocs.yml` 等配置文件中的一个小错误或语法错误造成的。

现在，在你创建一个可能会立即得到回复并关闭的错误报告之前，通过查阅相关文档章节或其他已报告或已关闭的问题或讨论，你可以为我们和你自己节省时间：

1.  [搜索我们的文档][Search our documentation]并查找与你的问题相关的部分。如果找到了，请确保你正确配置了一切。

1.  [搜索我们的问题跟踪器][issue tracker]，因为其他用户可能已经报告了相同的问题，并且可能已经有了已知的解决方法或修复。因此，无需创建新问题。

2.  [搜索我们的讨论板][discussion board]了解其他用户是否也在努力解决类似的问题，并与我们伟大的社区一起寻找解决方案。许多问题都在这里得到了解决。

__记下所有<u>搜索词</u>和<u>相关链接</u>，你将在错误报告中需要它们。__

  [^2]:
    我们在文档中使用的术语可能与您的不同，但我们的意思是相同的。当您在错误报告中包含搜索词和相关链接时，您帮助我们调整和改进文档。

---

在这一点上，当你仍然没有找到问题的解决方案时，我们鼓励你创建一个问题，因为现在很可能你遇到了我们还不知道的东西。阅读以下部分了解如何创建一个完整且有用的错误报告。

  [Search our documentation]: ?q=

## 问题模板 {#issue-template}

我们创建了一个新的问题模板，使错误报告过程尽可能简单且对我们的社区和我们更高效。这是我们回答和修复超过1,600个问题（并且还在增加）的经验结果，包括以下部分：

- [标题][Title]
- [上下文][Context] <small>可选</small>
- [错误描述][Bug description]
- [相关链接][Related links]
- [复现][Reproduction]
- [复现步骤][Steps to reproduce]
- [浏览器][Browser] <small>可选</small>
- [清单][Checklist]

  [Title]: #title
  [Context]: #context
  [Bug description]: #bug-description
  [Related links]: #related-links
  [Reproduction]: #reproduction
  [Steps to reproduce]: #steps-to-reproduce
  [Browser]: #browser
  [Checklist]: #checklist

### 标题 {#title}

一个好的标题应该简短且具有描述性。它应该是问题的一句话执行摘要，因此可以从标题中推断出你想报告的错误的影响和严重程度。

| <!-- --> | 示例  |
| -------- | -------- |
| :material-check:{ style="color: #4DB6AC" } __清晰__ | 内置 `typeset` 插件改变了导航标题优先于 `h1`
| :material-close:{ style="color: #EF5350" } __冗长__ | 内置 `typeset` 插件改变了导航标题优先于文档标题的优先级
| :material-close:{ style="color: #EF5350" } __不清晰__ | 标题不起作用
| :material-close:{ style="color: #EF5350" } __无用__ | 帮助

### 上下文 <small>可选</small> { #context }

在描述错误之前，你可以提供额外的上下文，以便我们了解你试图实现什么。解释你在使用 MkDocs 的 Material 的情况，以及你认为可能相关的内容。不要在这里写关于错误的内容。

> __为什么这可能有帮助__：有些错误只在特定的设置、环境或边缘情况下表现出来，例如，当你的文档包含成千上万的文档时。

### 错误描述 {#bug-description}

现在，来到你想报告的错误。提供一个清晰、集中、具体和简洁的错误总结。解释为什么你认为这是一个应该报告给 MkDocs 的 Material 的错误，而不是其依赖项的错误。坚持以下原则：

  [^3]:
    有时，用户在我们的[问题跟踪器][issue tracker]上报告的错误是由我们的上游依赖项引起的，包括[MkDocs]、[Python Markdown]、[Python Markdown Extensions]或第三方插件。一个好的经验法则是将[`theme.name`][theme.name]更改为`mkdocs`或`readthedocs`，并检查问题是否仍然存在。如果问题仍然存在，那么问题可能与 MkDocs 的 Material 无关，应该向上游报告。如果有疑问，使用我们的[讨论板][discussion board]寻求帮助。

-   __解释<u>什么</u>，而不是<u>如何</u>__ – 不要在这里解释[如何复现错误][Steps to reproduce]，我们会涉及到这一点。专注于尽可能清楚地表达问题及其影响。

-   __保持简短和简洁__ – 如果错误可以在一两句话中精确解释，那就完美了。不要夸大其词 – 维护者和未来的用户会感激你少读一些内容。

-   __一次报告一个错误__ – 如果你遇到几个不相关的错误，请为它们创建单独的问题。不要在同一个问题中报告它们，因为这会使归因变得困难。

---

:material-run-fast: __额外目标__ – 如果你找到了一个解决方法或修复错误的方法，你可以帮助其他用户在我们维护者能够在我们的代码库中修复错误之前临时缓解问题。

> __我们为什么需要这个__：为了我们能够理解问题，我们需要对其进行清晰的描述并量化其影响，这对于分级和优先级排序至关重要。

  [MkDocs]: https://www.mkdocs.org
  [Python Markdown]: https://python-markdown.github.io/extensions/
  [Python Markdown Extensions]: https://facelessuser.github.io/pymdown-extensions/
  [theme.name]: https://www.mkdocs.org/user-guide/configuration/#theme

### 相关链接 {#related-links}

当然，在报告错误之前，你已经阅读了我们的文档并[未能找到有效的解决方案][search for solutions]。请分享与错误相关的我们文档的所有部分的链接，这有助于我们逐步改进它。

此外，由于你在报告问题之前已经搜索过我们的[问题跟踪器][issue tracker]和[讨论板][discussion board]，并可能找到了几个问题或讨论，也请包括这些内容。每个问题或讨论的链接都会创建一个反向链接，为我们的维护者和未来的用户提供指导。

---

:material-run-fast: __延伸目标__ — 如果你还包括了在[寻找解决方案][search for solutions]时使用的搜索词，你就会让我们维护者更容易改进文档。

> __为什么我们需要这些__：相关链接帮助我们更好地理解你在尝试实现什么，以及我们的文档的哪些部分需要调整、扩展或彻底改写。

  [search for solutions]: #search-for-solutions

### 复现

一个最小化的复现是每一个写得好的错误报告的核心，因为它允许我们维护者立即重新创建必要的条件来检查错误，以快速找到其根本原因。有明确和简洁复现的问题可以更快得到解决。

[:material-bug: 创建复现][Create reproduction]{ .md-button .md-button--primary }

---

在你创建了复现后，你应该会有一个 `.zip` 文件，理想情况下不应大于 1 MB。只需将 `.zip` 文件拖放到此字段中，它将自动上传到 GitHub。

> __为什么我们需要这个__：如果一个问题不包含最小化复现，或者只是一个包含成千上万个文件的仓库的链接，维护者需要花费大量时间尝试重新创建正确的条件以检查错误，更不用说修复它了。

!!! warning "不要分享仓库链接"

    虽然我们知道在开发者中包含一个带有错误报告的仓库链接是一种好习惯，但我们目前在我们的流程中不支持这些。原因是自动生成的复现包含了通常被遗忘的所有必要的环境信息。

    此外，很多使用 MkDocs 的 Material 的非技术用户在创建仓库时会遇到困难。

  [Create reproduction]: ../guides/creating-a-reproduction.md
  [built-in info plugin]: ../plugins/info.md

### 复现步骤 {#steps-to-reproduce}

此时，你已经为我们提供了足够的信息来理解错误，并为我们提供了一个我们可以运行和检查的复现。然而，当我们运行你的复现时，可能不会立即明显我们如何可以看到错误发生。

因此，请列出我们在运行你的复现时应该遵循的具体步骤以观察错误。保持步骤简短且精确，确保不遗漏任何内容。使用简单的语言，就像你向一个五岁的孩子解释一样，并关注连续性。

> __为什么我们需要这个__：我们必须知道如何导航你的复现以观察错误，因为有些错误只在特定的视口或在特定条件下发生。

### 浏览器 <small>可选</small> {#browser}

如果你报告的错误只在一个或多个特定的浏览器中发生，我们需要知道哪些浏览器受到影响。此字段为可选，因为它只与当你报告的错误不涉及在[预览][previewing]或[构建][building]你的网站时崩溃相关。

---

:material-incognito: __隐身模式__ — 请验证错误是否不是由浏览器扩展引起的。切换到隐身模式并尝试复现错误。如果问题消失了，那么它是由一个扩展引起的。

> __为什么我们需要这个__：有些错误只在特定的浏览器或版本中发生。由于现在几乎所有的浏览器都是常绿的，我们通常不需要知道问题发生的版本，但我们可能稍后会询问。如果有疑问，请在上面的字段中首先添加浏览器版本。

  [previewing]: http://localhost:8000/mkdocs-material/creating-your-site/#previewing-as-you-write
  [building]: http://localhost:8000/mkdocs-material/creating-your-site/#building-your-site

### 清单 {#checklist}

感谢你遵循指南并创建了一个高质量且完整的错误报告——你几乎完成了。清单确保你已经阅读了这份指南，并已尽你所能提供了我们需要知道的一切信息来帮助你。

__我们将从这里接手。__
