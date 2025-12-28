# Google HTML/CSS 风格指南摘要 (Google HTML/CSS Style Guide Summary)

本文档总结了 Google HTML/CSS 风格指南中的关键规则和最佳实践。

## 1. 一般规则 (General Rules)
- **协议 (Protocol):** 对所有嵌入资源使用 HTTPS。
- **缩进 (Indentation):** 缩进 2 个空格。不要使用制表符 (Tab)。
- **大小写 (Capitalization):** 所有代码（元素名、属性、选择器、属性）仅使用小写。
- **尾随空格 (Trailing Whitespace):** 移除所有尾随空格。
- **编码 (Encoding):** 使用 UTF-8（无 BOM）。在 HTML 中指定 `<meta charset="utf-8">`。

## 2. HTML 风格规则 (HTML Style Rules)
- **文档类型 (Document Type):** 使用 `<!doctype html>`。
- **HTML 有效性 (HTML Validity):** 使用有效的 HTML。
- **语义 (Semantics):** 根据其预期用途使用 HTML 元素（例如，使用 `<p>` 表示段落，而不是用于间距）。
- **多媒体回退 (Multimedia Fallback):** 为图像提供 `alt` 文本，为音频/视频提供脚本/字幕。
- **关注点分离 (Separation of Concerns):** 严格分离结构 (HTML)、表现 (CSS) 和行为 (JavaScript)。从外部文件链接 CSS 和 JS。
- **`type` 属性 (`type` Attributes):** 省略样式表 (`<link>`) 和脚本 (`<script>`) 的 `type` 属性。

## 3. HTML 格式化规则 (HTML Formatting Rules)
- **常规 (General):** 每个块、列表或表格元素使用新行，并缩进其子元素。
- **引号 (Quotation Marks):** 属性值使用双引号 (`""`)。

## 4. CSS 风格规则 (CSS Style Rules)
- **CSS 有效性 (CSS Validity):** 使用有效的 CSS。
- **类命名 (Class Naming):** 使用有意义的、通用的名称。用连字符 (`-`) 分隔单词。
  - **好 (Good):** `.video-player`, `.site-navigation`
  - **坏 (Bad):** `.vid`, `.red-text`
- **ID 选择器 (ID Selectors):** 避免使用 ID 选择器进行样式设置。优先使用类选择器。
- **简写属性 (Shorthand Properties):** 尽可能使用简写属性（例如 `padding`, `font`）。
- **`0` 和单位 (`0` and Units):** 省略 `0` 值的单位（例如 `margin: 0;`）。
- **前导 `0` (Leading `0`s):** 小数值始终包含前导 `0`（例如 `font-size: 0.8em;`）。
- **十六进制表示法 (Hexadecimal Notation):** 尽可能使用 3 字符的十六进制表示法（例如 `#fff`）。
- **`!important`:** 避免使用 `!important`。

## 5. CSS 格式化规则 (CSS Formatting Rules)
- **声明顺序 (Declaration Order):** 规则内的声明按字母顺序排列。
- **缩进 (Indentation):** 缩进所有块内容。
- **分号 (Semicolons):** 在每个声明后使用分号。
- **间距 (Spacing):**
  - 属性名的冒号后使用空格 (`font-weight: bold;`)。
  - 最后一个选择器和左大括号之间使用空格 (`.foo {`)。
  - 每个选择器和声明开始新的一行。
- **规则分隔 (Rule Separation):** 用新行分隔规则。
- **引号 (Quotation Marks):** 属性选择器和属性值使用单引号 (`''`)（例如 `[type='text']`）。

**保持一致 (BE CONSISTENT)。** 编辑代码时，匹配现有风格。

*来源: [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)*
