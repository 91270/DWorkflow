# Google TypeScript 风格指南摘要 (Google TypeScript Style Guide Summary)

本文档总结了 Google TypeScript 风格指南中的关键规则和最佳实践，该指南由 `gts` 工具强制执行。

## 1. 语言特性 (Language Features)
- **变量声明 (Variable Declarations):** 始终使用 `const` 或 `let`。**禁止使用 `var`。** 默认使用 `const`。
- **模块 (Modules):** 使用 ES6 模块 (`import`/`export`)。**不要使用 `namespace`。**
- **导出 (Exports):** 使用命名导出 (`export {MyClass};`)。**不要使用默认导出 (default exports)。**
- **类 (Classes):**
  - **不要使用 `#private` 字段。** 使用 TypeScript 的 `private` 可见性修饰符。
  - 将在构造函数外部从未重新赋值的属性标记为 `readonly`。
  - **绝不要使用 `public` 修饰符**（它是默认的）。尽可能使用 `private` 或 `protected` 限制可见性。
- **函数 (Functions):** 对命名函数优先使用函数声明。对匿名函数/回调使用箭头函数。
- **字符串字面量 (String Literals):** 使用单引号 (`'`)。对于插值和多行字符串使用模板字面量 (`` ` ``)。
- **相等性检查 (Equality Checks):** 始终使用三等号 (`===`) 和不等号 (`!==`)。
- **类型断言 (Type Assertions):** **避免使用类型断言 (`x as SomeType`) 和非空断言 (`y!`)**。如果你必须使用它们，请提供明确的理由。

## 2. 禁止的特性 (Disallowed Features)
- **`any` 类型:** **避免使用 `any`**。优先使用 `unknown` 或更具体的类型。
- **包装对象 (Wrapper Objects):** 不要实例化 `String`, `Boolean`, 或 `Number` 包装类。
- **自动分号插入 (ASI):** 不要依赖它。**所有语句显式以分号结尾。**
- **`const enum`:** 不要使用 `const enum`。使用普通的 `enum` 代替。
- **`eval()` 和 `Function(...string)`:** 禁止。

## 3. 命名 (Naming)
- **`UpperCamelCase` (大驼峰):** 用于类、接口、类型、枚举和装饰器。
- **`lowerCamelCase` (小驼峰):** 用于变量、参数、函数、方法和属性。
- **`CONSTANT_CASE` (全大写):** 用于全局常量值，包括枚举值。
- **`_` 前缀/后缀:** **不要使用 `_` 作为标识符的前缀或后缀**，包括私有属性。

## 4. 类型系统 (Type System)
- **类型推断 (Type Inference):** 简单、明显的类型依赖类型推断。复杂类型要显式声明。
- **`undefined` 和 `null`:** 两者都支持。在项目中保持一致。
- **可选 vs. `|undefined`:** 优先使用可选参数和字段 (`?`)，而不是向类型添加 `|undefined`。
- **`Array<T>` 类型:** 简单类型使用 `T[]`。更复杂的联合类型使用 `Array<T>`（例如 `Array<string | number>`）。
- **`{}` 类型:** **不要使用 `{}`**。优先使用 `unknown`, `Record<string, unknown>`, 或 `object`。

## 5. 注释和文档 (Comments and Documentation)
- **JSDoc:** 使用 `/** JSDoc */` 进行文档说明，使用 `//` 进行实现注释。
- **冗余 (Redundancy):** **不要在 `@param` 或 `@return` 块中声明类型**（例如 `/** @param {string} user */`）。这在 TypeScript 中是多余的。
- **增加信息:** 注释必须增加信息，而不仅仅是复述代码。

*来源: [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)*
