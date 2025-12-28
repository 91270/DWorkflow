# Google JavaScript 风格指南摘要 (Google JavaScript Style Guide Summary)

本文档总结了 Google JavaScript 风格指南中的关键规则和最佳实践。

## 1. 源文件基础 (Source File Basics)
- **文件命名 (File Naming):** 全部小写，使用下划线 (`_`) 或破折号 (`-`)。扩展名必须是 `.js`。
- **文件编码 (File Encoding):** UTF-8。
- **空白 (Whitespace):** 仅使用 ASCII 水平空格 (0x20)。**禁止使用制表符 (Tab) 进行缩进。**

## 2. 源文件结构 (Source File Structure)
- 新文件应为 ES 模块 (`import`/`export`)。
- **导出 (Exports):** 使用命名导出 (`export {MyClass};`)。**不要使用默认导出 (default exports)。**
- **导入 (Imports):** 导入语句不要换行。导入路径中的 `.js` 扩展名是强制性的。

## 3. 格式化 (Formatting)
- **大括号 (Braces):** 所有控制结构（`if`, `for`, `while` 等）都必须使用大括号，即使是单行块。使用 K&R 风格（"Egyptian brackets"）。
- **缩进 (Indentation):** 每个新块 +2 个空格。
- **分号 (Semicolons):** 每个语句必须以分号结尾。
- **列限制 (Column Limit):** 80 个字符。
- **换行 (Line-wrapping):** 续行至少缩进 +4 个空格。
- **空白 (Whitespace):** 方法之间使用单空行。没有尾随空格。

## 4. 语言特性 (Language Features)
- **变量声明 (Variable Declarations):** 默认使用 `const`，如果需要重新赋值则使用 `let`。**禁止使用 `var`。**
- **数组字面量 (Array Literals):** 使用尾随逗号。不要使用 `Array` 构造函数。
- **对象字面量 (Object Literals):** 使用尾随逗号和简写属性。不要使用 `Object` 构造函数。
- **类 (Classes):** 不要使用 JavaScript getter/setter 属性 (`get name()`)。提供普通方法代替。
- **函数 (Functions):** 对于嵌套函数，优先使用箭头函数以保留 `this` 上下文。
- **字符串字面量 (String Literals):** 使用单引号 (`'`)。对于多行字符串或复杂插值，使用模板字面量 (`` ` ``)。
- **控制结构 (Control Structures):** 优先使用 `for-of` 循环。`for-in` 循环仅应用于字典式对象。
- **`this`:** 仅在类构造函数、方法或在其中定义的箭头函数中使用 `this`。
- **相等性检查 (Equality Checks):** 始终使用恒等运算符 (`===` / `!==`)。

## 5. 禁止的特性 (Disallowed Features)
- `with` 关键字。
- `eval()` 或 `Function(...string)`。
- 自动分号插入 (Automatic Semicolon Insertion)。
- 修改内置对象 (`Array.prototype.foo = ...`)。

## 6. 命名 (Naming)
- **类 (Classes):** `UpperCamelCase`（大驼峰）。
- **方法和函数 (Methods & Functions):** `lowerCamelCase`（小驼峰）。
- **常量 (Constants):** `CONSTANT_CASE`（全大写加下划线）。
- **非常量字段和变量 (Non-constant Fields & Variables):** `lowerCamelCase`（小驼峰）。

## 7. JSDoc
- 对所有类、字段和方法使用 JSDoc。
- 使用 `@param`, `@return`, `@override`, `@deprecated`。
- 类型注解包含在大括号中（例如 `/** @param {string} userName */`）。

*来源: [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)*
