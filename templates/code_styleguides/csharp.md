# C#/.NET 8 代码风格指南

本指南基于 [Microsoft C# 编码规范](https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/coding-style/coding-conventions) 和 [.NET 运行时工程标准](https://github.com/dotnet/runtime/blob/main/docs/coding-guidelines/coding-style.md)。

---

## 1. 命名规范 (Naming Conventions)

### 1.1 基本规则
*   **PascalCase**: 用于类 (Class)、接口 (Interface)、结构 (Struct)、枚举 (Enum)、委托 (Delegate)、方法 (Method)、属性 (Property)、事件 (Event)、常量 (Constant)。
*   **camelCase**: 用于局部变量 (Local Variable)、方法参数 (Parameter)、私有字段 (Private Field)。
*   **私有字段**: 必须以 `_` 前缀开头，使用 `_camelCase`。

```csharp
public class ClientPortal
{
    private readonly ILogger _logger; // 私有字段
    public string TenantId { get; set; } // 属性

    public void ValidateRequest(string requestId) // 方法和参数
    {
        var isValid = true; // 局部变量
    }
}
```

### 1.2 接口与泛型
*   **接口**: 必须以 `I` 开头（例如 `ICertificateService`）。
*   **泛型参数**: 使用 `T` 开头，且具有描述性（例如 `TRequest`, `TResponse`）。

## 2. 代码格式与布局 (Formatting)

*   **缩进**: 使用 4 个空格，**禁止使用 Tab**。
*   **大括号**: 所有控制块（`if`, `for`, `foreach`）**必须**包含大括号，且大括号独占一行（Allman 风格）。

```csharp
// 正确
if (isValid)
{
    DoSomething();
}

// 错误
if (isValid) DoSomething();
```

## 3. C# 12 / .NET 8 现代特性

### 3.1 文件范围命名空间 (File-scoped Namespaces)
减少缩进层级，默认使用文件范围命名空间。

```csharp
// 正确
namespace AutoSSL.Core.Services;

public class MyService { ... }

// 避免
namespace AutoSSL.Core.Services
{
    public class MyService { ... }
}
```

### 3.2 全局引用 (Global Usings)
将常用的命名空间（如 `System`, `System.Collections.Generic`, `Microsoft.Extensions.Logging`）放入 `GlobalUsings.cs` 文件中统一管理。

### 3.3 记录类型 (Records)
对于 DTO (Data Transfer Objects)、API 请求/响应模型，优先使用 `record` 类型以利用其不可变性和简洁语法。

```csharp
public record CreateCertificateRequest(string Domain, string Email);
```

### 3.4 模式匹配 (Pattern Matching)
优先使用 `is`, `switch` 表达式来替代复杂的 `if-else` 链。

```csharp
var statusText = status switch
{
    CertStatus.Active => "运行中",
    CertStatus.Expired => "已过期",
    _ => "未知"
};
```

## 4. 异步编程 (Async/Await)

*   **后缀**: 异步方法名应以 `Async` 结尾（例如 `GetCertificateAsync`）。
*   **配置**: 库代码中尽量使用 `.ConfigureAwait(false)`，应用层代码（Controller/Event Handler）可省略。
*   **避免**: 禁止使用 `Task.Result` 或 `.Wait()`，以防止死锁。始终使用 `await`。

## 5. 依赖注入与 API

*   **构造函数注入**: 显式声明依赖，避免使用 Service Locator 模式。
*   **Minimal API**: 对于简单的微服务节点，优先使用 Minimal API 定义路由。

```csharp
app.MapGet("/api/certs/{id}", async (ICertService service, string id) => 
{
    return await service.GetAsync(id);
});
```

## 6. 注释与文档

*   **XML 文档**: 公共 API（Controller, Service Interface）必须包含 `/// <summary>` XML 注释。
*   **行内注释**: 解释“为什么”这样做，而不是“在做什么”。

```csharp
/// <summary>
/// 根据订单 ID 强制续期证书。
/// </summary>
/// <param name="orderId">订单唯一标识</param>
/// <returns>续期任务 ID</returns>
public async Task<string> RenewCertificateAsync(string orderId)
{
    // 由于 CA 接口限制，此处需增加 5秒 延迟防止 429 错误
    await Task.Delay(5000); 
    ...
}
```
