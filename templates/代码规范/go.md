# Effective Go 风格指南摘要 (Effective Go Style Guide Summary)

本文档总结了官方 "Effective Go" 指南中关于编写地道 Go 代码的关键规则和最佳实践。

## 1. 格式化 (Formatting)
- **`gofmt`:** 所有 Go 代码 **必须** 使用 `gofmt` (或 `go fmt`) 进行格式化。这是一个不可协商的自动化标准。
- **缩进 (Indentation):** 使用制表符 (Tab) 进行缩进（`gofmt` 会处理这个问题）。
- **行长 (Line Length):** Go 没有严格的行长限制。让 `gofmt` 处理换行。

## 2. 命名 (Naming)
- **`MixedCaps`:** 对多单词名称使用 `MixedCaps`（大驼峰）或 `mixedCaps`（小驼峰）。不要使用下划线。
- **导出与未导出 (Exported vs. Unexported):** 以大写字母开头的名称是导出的（公共的）。以小写字母开头的名称是未导出的（私有的）。
- **包名 (Package Names):** 简短、简洁、单单词、小写的名称。
- **Getter:** 不要给 Getter 加上 `Get` 前缀。名为 `owner` 的字段的 Getter 应命名为 `Owner()`。
- **接口名 (Interface Names):** 单方法接口由方法名加上 `-er` 后缀命名（例如 `Reader`, `Writer`）。

## 3. 控制结构 (Control Structures)
- **`if`:** 条件周围没有括号。大括号是强制性的。可以包含初始化语句（例如 `if err := file.Chmod(0664); err != nil`）。
- **`for`:** Go 唯一的循环结构。统一了 `for` 和 `while`。使用 `for...range` 遍历切片、映射、字符串和通道。
- **`switch`:** 比 C 语言更通用。默认情况下 case 不会穿透 (fall through)（需显式使用 `fallthrough`）。可以在没有表达式的情况下使用，作为更清晰的 `if-else-if` 链。

## 4. 函数 (Functions)
- **多返回值 (Multiple Returns):** 函数可以返回多个值。这是返回结果和错误的标准方式（例如 `value, err`）。
- **命名结果参数 (Named Result Parameters):** 返回参数可以命名。这可以使代码更清晰、更简洁。
- **`defer`:** 安排一个函数调用在执行 `defer` 的函数返回之前立即运行。将其用于清理任务，如关闭文件。

## 5. 数据 (Data)
- **`new` 与 `make`:**
  - `new(T)`: 为类型 `T` 的新项分配内存，将其置零，并返回一个指针 (`*T`)。
  - `make(T, ...)`: 仅创建并初始化切片、映射和通道。返回类型 `T` 的初始化值（非指针）。
- **切片 (Slices):** 处理序列的首选方式。它们比数组更灵活。
- **映射 (Maps):** 使用 "comma ok" 惯用法检查键是否存在：`value, ok := myMap[key]`。

## 6. 接口 (Interfaces)
- **隐式实现 (Implicit Implementation):** 类型通过实现接口的方法来实现接口。不需要 `implements` 关键字。
- **小接口 (Small Interfaces):** 相比一个大接口，更喜欢许多小接口。标准库充满了单方法接口（例如 `io.Reader`）。

## 7. 并发 (Concurrency)
- **通过通信共享内存 (Share Memory By Communicating):** 这是核心哲学。不要通过共享内存来通信；相反，通过通信来共享内存。
- **Goroutines:** 轻量级、并发执行的函数。使用 `go` 关键字启动一个。
- **通道 (Channels):** 用于 goroutine 之间通信的类型化管道。使用 `make` 创建它们。

## 8. 错误 (Errors)
- **`error` 类型:** 内置的 `error` 接口是处理错误的标准方式。
- **显式错误处理 (Explicit Error Handling):** 不要使用空标识符 (`_`) 丢弃错误。显式检查错误。
- **`panic`:** 仅用于真正特殊的、不可恢复的情况。通常，库不应 panic。

*来源: [Effective Go](https://go.dev/doc/effective_go)*
