# Dart 代码风格指南 (Dart Code Style Guide)

本指南总结了官方 Effective Dart 文档中的关键建议，涵盖风格、文档、语言使用和 API 设计原则。遵守这些准则可促进 Dart 代码的一致性、可读性和可维护性。

## 1. 风格 (Style)

### 1.1. 标识符 (Identifiers)

- **务必 (DO)** 使用 `UpperCamelCase`（大驼峰命名法）命名类型、扩展和枚举类型。
- **务必 (DO)** 使用 `lowercase_with_underscores`（下划线小写命名法）命名包、目录和源文件。
- **务必 (DO)** 使用 `lowercase_with_underscores` 命名导入前缀。
- **务必 (DO)** 使用 `lowerCamelCase`（小驼峰命名法）命名其他标识符（类成员、顶层定义、变量、参数）。
- **推荐 (PREFER)** 使用 `lowerCamelCase` 命名常量。
- **务必 (DO)** 将超过两个字母的首字母缩略词像单词一样大写（例如 `Http`, `Nasa`, `Uri`）。两个字母的首字母缩略词（例如 `ID`, `TV`, `UI`）应保持全大写。
- **推荐 (PREFER)** 在匿名函数和局部函数中使用通配符 (`_`) 表示未使用的回调参数。
- **不要 (DON'T)** 对非私有标识符使用前导下划线。
- **不要 (DON'T)** 使用前缀字母（例如 `kDefaultTimeout` 中的 k）。
- **不要 (DON'T)** 使用 `library` 指令显式命名库。

### 1.2. 排序 (Ordering)

- **务必 (DO)** 将 `dart:` 导入放在其他导入之前。
- **务必 (DO)** 将 `package:` 导入放在相对导入之前。
- **务必 (DO)** 在所有导入之后的单独部分中指定导出 (`export`)。
- **务必 (DO)** 按字母顺序对各部分进行排序。

### 1.3. 格式化 (Formatting)

- **务必 (DO)** 使用 `dart format` 格式化你的代码。
- **考虑 (CONSIDER)** 更改你的代码以使其对格式化程序更友好（例如，缩短长标识符，简化嵌套表达式）。
- **推荐 (PREFER)** 每行不超过 80 个字符。
- **务必 (DO)** 对所有流控制语句（`if`, `for`, `while`, `do`, `try`, `catch`, `finally`）使用大括号。

## 2. 文档 (Documentation)

### 2.1. 注释 (Comments)

- **务必 (DO)** 将注释格式化为句子（首字母大写，以句号结尾）。
- **不要 (DON'T)** 使用块注释 (`/* ... */`) 进行文档说明；使用 `//` 进行常规注释。

### 2.2. 文档注释 (Doc Comments)

- **务必 (DO)** 使用 `///` 文档注释来记录成员和类型。
- **推荐 (PREFER)** 为公共 API 编写文档注释。
- **考虑 (CONSIDER)** 编写库级文档注释。
- **考虑 (CONSIDER)** 为私有 API 编写文档注释。
- **务必 (DO)** 以单句摘要开始文档注释。
- **务必 (DO)** 将文档注释的第一句分成单独的段落。
- **避免 (AVOID)** 与周围上下文冗余（例如，不要在文档注释中重复类名）。
- **推荐 (PREFER)** 如果函数或方法的主要目的是副作用（例如 "Connects to..."），则以第三人称动词开始注释。
- **推荐 (PREFER)** 以名词短语开始非布尔变量或属性的注释（例如 "The current day..."）。
- **推荐 (PREFER)** 以 "Whether" 后跟名词或动名词短语开始布尔变量或属性的注释（例如 "Whether the modal is..."）。
- **推荐 (PREFER)** 如果返回值是函数或方法的主要目的，则使用名词短语或非祈使动词短语。
- **不要 (DON'T)** 同时为属性的 getter 和 setter 编写文档。
- **推荐 (PREFER)** 以名词短语开始库或类型注释。
- **考虑 (CONSIDER)** 在文档注释中使用三重反引号包含代码示例。
- **务必 (DO)** 在文档注释中使用方括号 (`[]`) 引用作用域内的标识符（例如 `[StateError]`, `[anotherMethod()]`, `[Duration.inDays]`, `[Point.new]`）。
- **务必 (DO)** 使用散文解释参数、返回值和异常。
- **务必 (DO)** 将文档注释放在元数据注解之前。

### 2.3. Markdown

- **避免 (AVOID)** 过度使用 Markdown。
- **避免 (AVOID)** 使用 HTML 进行格式化。
- **推荐 (PREFER)** 使用反引号围栏 (```) 表示代码块。

### 2.4. 写作 (Writing)

- **推荐 (PREFER)** 简洁。
- **避免 (AVOID)** 缩写和首字母缩略词，除非它们显而易见。
- **推荐 (PREFER)** 使用 "this" 而不是 "the" 来指代成员的实例。

## 3. 使用 (Usage)

### 3.1. 库 (Libraries)

- **务必 (DO)** 在 `part of` 指令中使用字符串。
- **不要 (DON'T)** 导入另一个包 `src` 目录内的库。
- **不要 (DON'T)** 允许导入路径伸入或伸出 `lib`。
- **推荐 (PREFER)** 在不跨越 `lib` 边界时使用相对导入路径。

### 3.2. 空安全 (Null Safety)

- **不要 (DON'T)** 显式将变量初始化为 `null`。
- **不要 (DON'T)** 使用显式的默认值 `null`。
- **不要 (DON'T)** 在相等运算中使用 `true` 或 `false`（例如 `if (nonNullableBool == true)`）。
- **避免 (AVOID)** 如果你需要检查变量是否已初始化，请避免使用 `late` 变量；推荐使用可空类型。
- **考虑 (CONSIDER)** 使用类型提升或空检查模式来使用可空类型。

### 3.3. 字符串 (Strings)

- **务必 (DO)** 使用相邻字符串连接字符串字面量。
- **推荐 (PREFER)** 使用插值 (`$variable`, `${expression}`) 组合字符串和值。
- **避免 (AVOID)** 在不需要时在插值中使用大括号（例如，使用 `'$name'` 而不是 `'${name}'`）。

### 3.4. 集合 (Collections)

- **务必 (DO)** 尽可能使用集合字面量 (`[]`, `{}`, `<type>{}`)。
- **不要 (DON'T)** 使用 `.length` 检查集合是否为空；使用 `.isEmpty` 或 `.isNotEmpty`。
- **避免 (AVOID)** 使用带有函数字面量的 `Iterable.forEach()`；推荐 `for-in` 循环。
- **不要 (DON'T)** 使用 `List.from()`，除非你打算更改结果的类型；推荐 `.toList()`。
- **务必 (DO)** 使用 `whereType()` 按类型过滤集合。
- **避免 (AVOID)** 当附近的操作（如 `List<T>.from()` 或 `map<T>()`）可以完成时使用 `cast()`。

### 3.5. 函数 (Functions)

- **务必 (DO)** 使用函数声明将函数绑定到名称。
- **不要 (DON'T)** 当 tear-off（直接引用函数名）可以完成时创建 lambda（例如，使用 `list.forEach(print)` 而不是 `list.forEach((e) => print(e))`）。

### 3.6. 变量 (Variables)

- **务必 (DO)** 对局部变量的 `var` 和 `final` 遵循一致的规则（对于未重新赋值的使用 `final`，对于重新赋值的使用 `var`；或者对所有局部变量使用 `var`）。
- **避免 (AVOID)** 存储你可以计算的内容（例如，如果你有 `radius`，不要存储 `area`）。

### 3.7. 成员 (Members)

- **不要 (DON'T)** 不必要地将字段包装在 getter 和 setter 中。
- **推荐 (PREFER)** 使用 `final` 字段创建只读属性。
- **考虑 (CONSIDER)** 对简单成员（getter、setter、单表达式方法）使用 `=>`。
- **不要 (DON'T)** 使用 `this.`，除非为了重定向到命名构造函数或避免遮蔽。
- **务必 (DO)** 尽可能在声明时初始化字段。

### 3.8. 构造函数 (Constructors)

- **务必 (DO)** 尽可能使用初始化形式参数 (`this.field`)。
- **不要 (DON'T)** 当构造函数初始化列表可以完成时使用 `late`。
- **务必 (DO)** 对空构造函数体使用 `;` 而不是 `{}`。
- **不要 (DON'T)** 使用 `new`。
- **不要 (DON'T)** 在常量上下文中冗余地使用 `const`。

### 3.9. 错误处理 (Error Handling)

- **避免 (AVOID)** 没有 `on` 子句的 `catch` 子句。
- **不要 (DON'T)** 丢弃来自没有 `on` 子句的 `catch` 子句的错误。
- **务必 (DO)** 仅针对编程错误抛出实现 `Error` 的对象。
- **不要 (DON'T)** 显式捕获 `Error` 或实现它的类型。
- **务必 (DO)** 使用 `rethrow` 重新抛出捕获的异常以保留原始堆栈跟踪。

### 3.10. 异步 (Asynchrony)

- **推荐 (PREFER)** `async`/`await` 优于使用原始 `Future`。
- **不要 (DON'T)** 当 `async` 没有有用效果时使用它。
- **考虑 (CONSIDER)** 使用高阶方法转换流。
- **避免 (AVOID)** 直接使用 `Completer`。

## 4. API 设计 (API Design)

### 4.1. 名称 (Names)

- **务必 (DO)** 始终如一地使用术语。
- **避免 (AVOID)** 缩写，除非比未缩写的术语更常用。
- **推荐 (PREFER)** 将最具描述性的名词放在最后（例如 `pageCount`）。
- **考虑 (CONSIDER)** 使代码在使用 API 时读起来像一个句子。
- **推荐 (PREFER)** 对非布尔属性或变量使用名词短语。
- **推荐 (PREFER)** 对布尔属性或变量使用非祈使动词短语（例如 `isEnabled`, `canClose`）。
- **考虑 (CONSIDER)** 对命名布尔参数省略动词（例如 `growable: true`）。
- **推荐 (PREFER)** 对布尔属性或变量使用“肯定”名称（例如 `isConnected` 优于 `isDisconnected`）。
- **推荐 (PREFER)** 如果函数或方法的主要目的是副作用，则使用祈使动词短语（例如 `list.add()`, `window.refresh()`）。
- **推荐 (PREFER)** 如果返回值是其主要目的，则对函数或方法使用名词短语或非祈使动词短语（例如 `list.elementAt(3)`）。
- **考虑 (CONSIDER)** 如果你想引起对执行工作的注意，则对函数或方法使用祈使动词短语（例如 `database.downloadData()`）。
- **避免 (AVOID)** 以 `get` 开头的方法名。
- **推荐 (PREFER)** 如果方法将对象的状态复制到新对象，则命名为 `to___()`（例如 `toList()`）。
- **推荐 (PREFER)** 如果方法返回由原始对象支持的不同表示形式，则命名为 `as___()`（例如 `asMap()`）。
- **避免 (AVOID)** 在函数或方法的名称中描述参数。
- **务必 (DO)** 在命名类型参数时遵循现有的助记符约定（例如 `E` 表示元素，`K`, `V` 表示映射键/值，`T`, `S`, `U` 表示通用类型）。

### 4.2. 库 (Libraries)

- **推荐 (PREFER)** 将声明设为私有 (`_`)。
- **考虑 (CONSIDER)** 如果多个类在逻辑上属于同一类，则在同一库中声明它们。

### 4.3. 类和 Mixin (Classes and Mixins)

- **避免 (AVOID)** 当简单函数 (`typedef`) 可以完成时定义单成员抽象类。
- **避免 (AVOID)** 定义仅包含静态成员的类；推荐顶层函数/变量或库。
- **避免 (AVOID)** 扩展不打算被子类化的类。
- **务必 (DO)** 使用类修饰符（例如 `final`, `interface`, `sealed`）来控制你的类是否可以扩展。
- **避免 (AVOID)** 实现不打算作为接口的类。
- **务必 (DO)** 使用类修饰符来控制你的类是否可以作为接口。
- **推荐 (PREFER)** 定义纯 mixin 或纯类，而不是 `mixin class`。

### 4.4. 构造函数 (Constructors)

- **考虑 (CONSIDER)** 如果类支持（所有字段都是 `final` 且在构造函数中初始化），则将构造函数设为 `const`。

### 4.5. 成员 (Members)

- **推荐 (PREFER)** 将字段和顶层变量设为 `final`。
- **务必 (DO)** 将 getter 用于概念上访问属性的操作（无参数，返回结果，无用户可见的副作用，幂等）。
- **务必 (DO)** 将 setter 用于概念上更改属性的操作（单个参数，无结果，更改状态，幂等）。
- **不要 (DON'T)** 定义没有相应 getter 的 setter。
- **避免 (AVOID)** 使用运行时类型测试来伪造重载。
- **避免 (AVOID)** 没有初始化器的公共 `late final` 字段。
- **避免 (AVOID)** 返回可空的 `Future`, `Stream`, 和集合类型；推荐空容器或可空类型的非空 future。
- **避免 (AVOID)** 仅为了启用流式接口而从方法返回 `this`；推荐方法级联。

### 4.6. 类型 (Types)

- **务必 (DO)** 对没有初始化器的变量进行类型注解。
- **务必 (DO)** 如果类型不明显，则对字段和顶层变量进行类型注解。
- **不要 (DON'T)** 对已初始化的局部变量进行冗余类型注解。
- **务必 (DO)** 在函数声明上注解返回类型。
- **务必 (DO)** 在函数声明上注解参数类型。
- **不要 (DON'T)** 在函数表达式上注解推断的参数类型。
- **不要 (DON'T)** 对初始化形式参数进行类型注解。
- **务必 (DO)** 在未推断的泛型调用上编写类型参数。
- **不要 (DON'T)** 在推断的泛型调用上编写类型参数。
- **避免 (AVOID)** 编写不完整的泛型类型。
- **务必 (DO)** 用 `dynamic` 注解，而不是让推断静默失败。
- **推荐 (PREFER)** 函数类型注解中的签名。
- **不要 (DON'T)** 为 setter 指定返回类型。
- **不要 (DON'T)** 使用传统的 `typedef` 语法。
- **推荐 (PREFER)** 内联函数类型优于 `typedef`。
- **推荐 (PREFER)** 对参数使用函数类型语法。
- **避免 (AVOID)** 使用 `dynamic`，除非你想禁用静态检查。
- **务必 (DO)** 使用 `Future<void>` 作为不产生值的异步成员的返回类型。
- **避免 (AVOID)** 使用 `FutureOr<T>` 作为返回类型。

### 4.7. 参数 (Parameters)

- **避免 (AVOID)** 位置布尔参数。
- **避免 (AVOID)** 可选位置参数，如果用户可能想省略前面的参数。
- **避免 (AVOID)** 接受特殊“无参数”值的强制参数。
- **务必 (DO)** 使用包含起始和排除结束的参数来接受范围。

### 4.8. 相等性 (Equality)

- **务必 (DO)** 如果你重写 `==`，则重写 `hashCode`。
- **务必 (DO)** 使你的 `==` 运算符遵守相等的数学规则（自反性、对称性、传递性、一致性）。
- **避免 (AVOID)** 为可变类定义自定义相等性。
- **不要 (DON'T)** 使 `==` 的参数可空。

_来源:_

- [Effective Dart: 风格](https://dart.dev/effective-dart/style)
- [Effective Dart: 文档](https://dart.dev/effective-dart/documentation)
- [Effective Dart: 使用](https://dart.dev/effective-dart/usage)
- [Effective Dart: 设计](https://dart.dev/effective-dart/design)