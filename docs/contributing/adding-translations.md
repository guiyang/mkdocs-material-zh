# 翻译 {#translations}

难以置信 — 在国际社区贡献的帮助下，MkDocs 的 Material 已被翻译成60多种语言。正如你可以想象的，对我们维护者来说，保持所有语言的更新是不可能的，新功能有时需要新的翻译。

如果你想帮助我们使 MkDocs 的 Material 更加全球化，并且注意到你的语言缺少翻译，或者你想添加新的语言，你可以按照下面的指南帮助我们。

## 在创建问题之前 {#before-creating-an-issue}

翻译经常变更，这就是为什么我们想确保你不会在重复工作中投入时间。在添加翻译之前，请检查以下事项：

### 检查语言可用性 {#check-language-availability}

已经支持60多种语言，很有可能你的语言已经由 MkDocs 的 Material 支持了。你可以通过检查[支持的语言][supported languages]列表来查看你的语言是否可用，或者是否需要改进或额外的翻译：

- __你的语言已经得到支持__ — 在这种情况下，你可以检查是否有翻译缺失，并点击你语言下的链接添加它们，这只需要5分钟。

- __你的语言缺失__ — 在这种情况下，你可以帮助我们为 MkDocs 的 Material 添加对你的语言的支持！继续阅读，学习如何做到这一点。

  [supported languages]: ../setup/changing-the-language.md#site-language

### 搜索我们的问题跟踪器 {#search-our-issue-tracker}

可能已经有其他用户创建了问题，提供了你的语言缺失的翻译，这些翻译仍然需要我们维护者整合。为了避免你在重复工作中投入时间，请事先搜索[问题跟踪器][issue tracker]。

  [issue tracker]: https://github.com/squidfunk/mkdocs-material/issues

---

此时，当你确定 MkDocs 的 Material 还没有支持你的语言时，你可以按照问题模板添加新的翻译。

## 问题模板 {#issue-template}

我们创建了一个问题模板，使贡献翻译尽可能简单。这是我们在过去几年中处理60多种语言的贡献和更新的经验结果，包括以下部分：

- [标题][Title]
- [翻译][Translations]
- [国家旗帜][Country flag] <small>可选</small>
- [清单][Checklist]

  [Title]: #title
  [Translations]: #translations
  [Country flag]: #country-flag
  [Checklist]: #checklist

### 标题 {#title}

当你更新已存在的语言时，你可以保留标题原样。添加对新语言的支持时，将预填标题中的`...`替换为你的语言名称。

| <!-- --> | 示例  |
| -------- | -------- |
| :material-check:{ style="color: #4DB6AC" } __清晰__ | 为德语添加翻译
| :material-close:{ style="color: #EF5350" } __不清晰__ | 添加翻译...
| :material-close:{ style="color: #EF5350" } __无用__ | 帮助

### 翻译 {#translations}

如果翻译旁边有一个 :arrow_left: 图标，表示它缺失。你可以翻译这一行并移除 :arrow_left: 图标。如果你不知道如何翻译特定行，简单地留给其他贡献者完成。为确保翻译的准确性，请通过查看我们的[英文翻译][English translations]来双重检查词汇的上下文。

[English translations]: https://github.com/squidfunk/mkdocs-material/tree/master/src/partials/languages/en.html

### 国家旗帜 <small>可选</small> { #country-flag }

为了更好地概览，我们的[支持的语言][supported languages]列表在语言名称旁边包括了国家旗帜。你可以通过在此字段添加国家旗帜的短代码来帮助我们为你的语言选择一个旗帜。前往我们的[表情符号搜索][emoji search]并输入`flag`来查找所有可用的短代码。

!!! question "如果我的旗帜不可用怎么办？"

    [Twemoji]为260个国家提供了旗帜表情符号 -- 不支持国家的细分，如州、省或地区。如果你为一个细分地区添加翻译，请选择最合适的可用旗帜。

  [Twemoji]: https://twemoji.twitter.com/
  [emoji search]: ../reference/icons-emojis.md#search

> __为什么这可能有帮助__：在国家名称旁边添加国家旗帜可以帮助你和其他人更快更容易地在支持的语言列表中找到该语言。如果你的国家的旗帜不被[Twemoji]支持，你可以帮助我们选择一个替代品。

### 清单 {#checklist}

感谢你遵循指南并帮助我们为 MkDocs 的 Material 添加新的翻译 — 你快完成了。清单确保你已经阅读了这份指南，并已尽你所能提供了我们需要的所有信息来整合你的贡献。

__我们将从这里接手。__

---

## 归属 {#attribution}

如果你使用上面的模板提交了翻译，你将作为共同作者在提交中被记入名单，所以你不需要开启一个拉取请求。你对项目做出了重大贡献，使 MkDocs 的 Material 能够为世界上更多的人提供服务。谢谢你！
