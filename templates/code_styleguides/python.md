# Google Python 风格指南摘要 (Google Python Style Guide Summary)

本文档总结了 Google Python 风格指南中的关键规则和最佳实践。

## 1. Python 语言规则 (Python Language Rules)
- **Linting:** 在代码上运行 `pylint` (或 `ruff`, `flake8`) 以捕获错误和风格问题。
- **导入 (Imports):** 使用 `import x` 导入包/模块。仅当 `y` 是子模块时使用 `from x import y`。
- **异常 (Exceptions):** 使用内置异常类。不要使用裸 `except:` 子句（必须指定异常类型）。
- **全局状态 (Global State):** 避免可变的全局状态。模块级常量是可以的，应使用 `ALL_CAPS_WITH_UNDERSCORES` 命名。
- **推导式 (Comprehensions):** 用于简单的情况。避免用于复杂逻辑，此时完整的循环更具可读性。
- **默认参数值 (Default Argument Values):** 不要使用可变对象（如 `[]` 或 `{}`）作为默认值。
- **True/False 评估:** 使用隐式 False（例如 `if not my_list:`）。使用 `if foo is None:` 检查 `None`。
- **类型注解 (Type Annotations):** 强烈鼓励对所有公共 API 使用类型注解。

## 2. Python 风格规则 (Python Style Rules)
- **行长 (Line Length):** 最多 80 个字符。
- **缩进 (Indentation):** 每个缩进级别 4 个空格。绝不要使用制表符 (Tab)。
- **空行 (Blank Lines):** 顶级定义（类、函数）之间空两行。方法定义之间空一行。
- **空白 (Whitespace):** 避免多余的空白。二元运算符周围使用单个空格。
- **文档字符串 (Docstrings):** 使用 `"""三重双引号"""`。每个公共模块、函数、类和方法都必须有文档字符串。
  - **格式:** 以一行摘要开始。包括 `Args:`, `Returns:`, 和 `Raises:` 部分。
- **字符串 (Strings):** 使用 f-strings 进行格式化。保持单引号 (`'`) 或双引号 (`"`) 一致。
- **`TODO` 注释:** 使用 `TODO(username): Fix this.` 格式。
- **导入格式化 (Imports Formatting):** 导入应在单独的行上并分组：标准库、第三方库和你自己的应用程序导入。

## 3. 命名 (Naming)
- **常规:** 模块、函数、方法和变量使用 `snake_case`（下划线小写）。
- **类:** `PascalCase`（大驼峰）。
- **常量:** `ALL_CAPS_WITH_UNDERSCORES`（全大写加下划线）。
- **内部使用:** 对内部模块/类成员使用单个前导下划线（`_internal_variable`）。

## 4. Main
- 所有可执行文件都应有一个 `main()` 函数包含主要逻辑，并通过 `if __name__ == '__main__':` 块调用。

**保持一致 (BE CONSISTENT)。** 编辑代码时，匹配现有风格。

*来源: [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)*
