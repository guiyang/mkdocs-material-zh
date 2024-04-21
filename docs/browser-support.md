# 浏览器支持 {#browser-support}

Material for MkDocs 努力支持尽可能广泛的浏览器范围，同时通过现代 CSS 功能如 [自定义属性] 和 [遮罩图像] 保留简单的自定义可能性。

  [自定义属性]: https://caniuse.com/css-variables
  [遮罩图像]: https://caniuse.com/mdn-css_properties_mask-image

## 支持的浏览器 {#supported-browsers}

以下表格列出了 Material for MkDocs 提供全面支持的所有浏览器，因此可以假设所有功能都能在这些浏览器中正常工作而不会退化。如果您发现在支持版本范围内的某个浏览器中某些内容看起来不正确，请[提交问题]：

<figure markdown>

| Browser                              | Version | Release date |         |        |      Usage |
| ------------------------------------ | ------: | -----------: | ------: | -----: | ---------: |
|                                      |         |              | desktop | mobile |    overall |
| :fontawesome-brands-chrome: Chrome   |     49+ |      03/2016 | 25.65%  | 38.33% |     63.98% |
| :fontawesome-brands-safari: Safari   |     10+ |      09/2016 |  4.63%  | 14.96% |     19.59% |
| :fontawesome-brands-edge: Edge       |     79+ |      01/2020 |  3.95%  |    n/a |      3.95% |
| :fontawesome-brands-firefox: Firefox |     53+ |      04/2017 |  3.40%  |   .30% |      3.70% |
| :fontawesome-brands-opera: Opera     |     36+ |      03/2016 |  1.44%  |   .01% |      1.45% |
|                                      |         |              |         |        | __92.67%__ |

  <figcaption markdown>

浏览器支持矩阵来源于 [caniuse.com]。[^1]

  </figcaption>
</figure>

  [^1]:
    数据收集自 [caniuse.com]，于2022年1月，并主要基于对 [自定义属性]、[遮罩图像] 和 [:is pseudo selector] 的浏览器支持，这些功能不完全可填充。市场份额少于1%的浏览器未被考虑，但它们可能仍然完全或部分支持。

请注意，使用数据基于全球浏览器市场份额，因此实际上可能与您的目标人群完全不同。检查用户中浏览器类型和版本的分布是一个好主意。

  [提交问题]: https://github.com/squidfunk/mkdocs-material/issues/new/choose
  [caniuse.com]: https://caniuse.com/
  [:is pseudo selector]: https://caniuse.com/css-matches-pseudo
  [browser support]: #supported-browsers
  [built-in privacy plugin]: plugins/privacy.md

## 其他浏览器 {#other-browsers}

尽管您的网站在现代浏览器上看起来可能不完美，以下较旧的浏览器版本可能需要一些额外努力才能工作：

- :fontawesome-brands-firefox: __Firefox 31-52__ – 由于缺少对 [遮罩图像] 的支持，图标将显示为小方框。虽然这无法填充，但可以通过完全隐藏图标来缓解。
- :fontawesome-brands-edge: __Edge 16-18__ – 由于缺少对 [:is pseudo selector] 的支持，某些元素的间距可能会有点不准确，这可以通过一些额外的努力来缓解。
- :fontawesome-brands-internet-explorer: __Internet Explorer__ - 不支持，主要是由于缺少对 [自定义属性] 的支持。Material for MkDocs 支持 Internet Explorer 的最后版本是
  <!-- md:version 4.6.3 -->.
