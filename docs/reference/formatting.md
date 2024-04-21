---
icon: material/format-font
---

# 格式化 Formatting {#formatting}

Material for MkDocs 支持多种 HTML 元素，可以用来突出文档的部分或应用特定格式。此外，还支持 [Critic Markup]，增加了显示文档建议更改的能力。

  [Critic Markup]: https://github.com/CriticMarkup/CriticMarkup-toolkit

## 配置 {#configuration}

此配置启用对键盘按键的支持、跟踪文档更改、定义下标和上标以及高亮文本。将以下行添加到 `mkdocs.yml`：

``` yaml
markdown_extensions:
  - pymdownx.critic
  - pymdownx.caret
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.tilde
```

查看其他配置选项：

- [Critic]
- [Caret, Mark & Tilde]
- [Keys]

  [Critic]: ../setup/extensions/python-markdown-extensions.md#critic
  [Caret, Mark & Tilde]: ../setup/extensions/python-markdown-extensions.md#caret-mark-tilde
  [Keys]: ../setup/extensions/python-markdown-extensions.md#keys

## 用法 {#usage}

### 高亮更改 {#highlighting-changes}

当启用 [Critic] 时，可以使用 [Critic Markup]，它增加了高亮建议更改的能力，并且可以向文档添加内联评论：

``` title="Text with suggested changes"
Text can be {--deleted--} and replacement text {++added++}. This can also be
combined into {~~one~>a single~~} operation. {==Highlighting==} is also
possible {>>and comments can be added inline<<}.

{==

Formatting can also be applied to blocks by putting the opening and closing
tags on separate lines and adding new lines between the tags and the content.

==}
```

<div class="result" markdown>

Text can be <del class="critic">deleted</del> and replacement text
<ins class="critic">added</ins>. This can also be combined into
<del class="critic">one</del><ins class="critic">a single</ins> operation.
<mark class="critic">Highlighting</mark> is also possible
<span class="critic comment">and comments can be added inline</span>.

<div>
  <mark class="critic block">
    <p>
      Formatting can also be applied to blocks by putting the opening and
      closing tags on separate lines and adding new lines between the tags and
      the content.
    </p>
  </mark>
</div>

</div>

### 高亮文本 {#highlighting-text}

当启用 [Caret, Mark & Tilde] 时，可以使用简单语法高亮文本，这比直接使用相应的 [`mark`][mark]、[`ins`][ins] 和 [`del`][del] HTML 标签更方便：

``` title="Text with highlighting"
- ==这是标记的==
- ^^这是插入的^^
- ~~这是删除的~~
```

<div class="result" markdown>

- ==这是标记的==
- ^^这是插入的^^
- ~~这是删除的~~

</div>

  [mark]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark
  [ins]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ins
  [del]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/del

### 下标和上标 {#sub-and-superscripts}

当启用 [Caret & Tilde][Caret, Mark & Tilde] 时，可以使用简单语法实现文本的下标和上标，这比直接使用相应的 [`sub`][sub] 和 [`sup`][sup] HTML 标签更方便：

``` markdown title="Text with sub- and superscripts"
- H~2~O
- A^T^A
```

<div class="result" markdown>

- H~2~O
- A^T^A

</div>

  [sub]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sub
  [sup]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sup

### 添加键盘按键 {#adding-keyboard-keys}

当启用 [Keys] 时，可以使用简单语法渲染键盘按键。请查阅 [Python Markdown 扩展包] 文档以了解所有可用的简码：

``` markdown title="Keyboard keys"
++ctrl+alt+del++
```

<div class="result" markdown>

++ctrl+alt+del++

</div>

  [Python Markdown 扩展包]: https://facelessuser.github.io/pymdown-extensions/extensions/keys/#extendingmodifying-key-map-index
