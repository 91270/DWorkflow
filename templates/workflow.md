# 项目工作流 (Project Workflow)

## Guiding Principles (指导原则)

1. **Plan 是单一事实来源：** 所有工作必须在 `plan.md` 中追踪。
2. **技术架构是经过深思熟虑的：** 对技术架构的更改必须在实现 *之前* 记录在 `技术架构.md` 中。
3. **测试驱动开发 (TDD)：** 在实现功能之前编写单元测试。
4. **高代码覆盖率：** 目标是所有模块的代码覆盖率 >80%。
5. **用户体验优先：** 每一个决定都应优先考虑用户体验。
6. **非交互式 & CI 感知：** 首选非交互式命令。对监视模式工具（测试、linter）使用 `CI=true` 以确保持单次执行。
7. **语言一致性：** 所有文档、代码注释（非核心逻辑）、Git Commit Message 和 Git Notes 必须使用简体中文。

## Task Workflow (任务工作流)

所有任务遵循严格的生命周期：

### 标准任务工作流

1. **选择任务：** 按顺序从 `plan.md` 中选择下一个可用任务。

2. **标记为进行中：** 在开始工作之前，编辑 `plan.md` 并将任务从 `[ ]` 更改为 `[~]`。

3. **编写失败测试 (Red Phase - 红灯阶段):**
   - 为 Feature 或 Bug fix 创建一个新的测试文件。
   - 编写一个或多个单元测试，清楚地定义任务的预期行为和验收标准。
   - **CRITICAL:** 运行测试并确认它们按预期失败。这是 TDD 的 "Red" 阶段。在拥有失败的测试之前，不要继续。

4. **实现以通过测试 (Green Phase - 绿灯阶段):**
   - 编写使失败测试通过所需的最少量的应用程序代码。
   - 再次运行测试套件并确认所有测试现在都通过。这是 "Green" 阶段。

5. **重构 (可选但推荐):**
   - 在通过测试的安全保障下，重构实现代码和测试代码以提高清晰度、消除重复并增强性能，而不改变外部行为。
   - 重构后重新运行测试以确它们仍然通过。

6. **验证覆盖率：** 使用项目选择的工具运行覆盖率报告。例如，在 Python 项目中，这可能如下所示：
   ```bash
   pytest --cov=app --cov-report=html
   ```
   目标：新代码覆盖率 >80%。具体工具和命令将因语言和框架而异。

7. **记录偏差：** 如果实现与技术架构不同：
   - **停止** 实现
   - 使用新设计更新 `技术架构.md`
   - 添加注明日期的说明解释更改
   - 恢复实现

8. **提交代码更改：**
   - 暂存 (Stage) 与任务相关的所有代码更改。
   - 提议一个清晰、简洁的 Commit Message，**必须使用中文 Type**，例如：`新增: 创建计算器的基本 HTML 结构`。
   - 执行提交。

9. **附加任务摘要 (Git Notes):**
   - **步骤 9.1: 获取 Commit Hash:** 获取 *刚刚完成的 commit* 的 hash (`git log -1 --format="%H"`)。
   - **步骤 9.2: 起草 Note 内容:** 为完成的任务创建一个详细摘要。这应包括任务名称、更改摘要、所有创建/修改文件的列表以及更改的核心“原因”。**Note 内容必须完全使用中文。**
   - **步骤 9.3: 附加 Note:** 使用 `git notes` 命令将摘要附加到 Commit。
     ```bash
     # 上一步的 note 内容通过 -m 标志传递。
     git notes add -m "<note content>" <commit_hash>
     ```

10. **获取并记录任务 Commit SHA:**
    - **步骤 10.1: 更新 Plan:** 阅读 `plan.md`，找到完成任务的行，将其状态从 `[~]` 更新为 `[x]`，并追加 *刚刚完成的 commit* 的 commit hash 的前 7 个字符。
    - **步骤 10.2: 写入 Plan:** 将更新的内容写回 `plan.md`。

11. **提交 Plan 更新：**
    - **行动：** 暂存修改后的 `plan.md` 文件。
    - **行动：** 使用描述性消息提交此更改（例如，`杂项: 标记任务 '创建用户模型' 为完成`）。

### 阶段完成验证与检查点协议 (Phase Completion Verification and Checkpointing Protocol)

**触发器：** 此协议在完成一个任务且该任务同时也结束了 `plan.md` 中的一个 Phase 后立即执行。

1.  **宣布协议开始：** 通知用户该阶段已完成，验证和检查点协议已开始。

2.  **确保阶段更改的测试覆盖率：**
    -   **步骤 2.1: 确定阶段范围：** 要识别在此阶段更改的文件，你必须首先找到起点。阅读 `plan.md` 以找到 *上一个* 阶段检查点的 Git Commit SHA。如果不存在上一个检查点，则范围是自第一次提交以来的所有更改。
    -   **步骤 2.2: 列出更改的文件：** 执行 `git diff --name-only <previous_checkpoint_sha> HEAD` 以获取在此阶段修改的所有文件的精确列表。
    -   **步骤 2.3: 验证并创建测试：** 对于列表中的每个文件：
        -   **CRITICAL:** 首先，检查其扩展名。排除非代码文件（例如 `.json`, `.md`, `.yaml`）。
        -   对于每个剩余的代码文件，验证是否存在相应的测试文件。
        -   如果测试文件缺失，你 **必须** 创建一个。在编写测试之前，**首先分析存储库中的其他测试文件以确定正确的命名约定和测试风格。** 新测试 **必须** 验证此阶段任务 (`plan.md`) 中描述的功能。

3.  **执行自动化测试与主动调试：**
    -   在执行之前，你 **必须** 宣布你将用于运行测试的确切 shell 命令。
    -   **示例公告：** “我现在将运行自动化测试套件以验证该阶段。**命令：** `CI=true npm test`”
    -   执行宣布的命令。
    -   如果测试失败，你 **必须** 通知用户并开始调试。你最多可以尝试提议 **两次** 修复。如果两次提议修复后测试仍然失败，你 **必须停止**，报告持续的失败，并询问用户指导。

4.  **提议详细、可操作的手动验证计划：**
    -   **CRITICAL:** 要生成计划，首先分析 `产品手册.md`, `设计规范.md`, 和 `plan.md` 以确定完成阶段的面向用户的目标。
    -   你 **必须** 生成一个分步计划，引导用户完成验证过程，包括任何必要的命令和具体的预期结果。
    -   你向用户展示的计划 **必须** 遵循此格式：

        **对于前端更改：**
        ```
        自动化测试已通过。对于手动验证，请遵循以下步骤：

        **手动验证步骤：**
        1.  **使用命令启动开发服务器：** `npm run dev`
        2.  **在浏览器中打开：** `http://localhost:3000`
        3.  **确认你看到：** 新的用户个人资料页面，正确显示用户的姓名和电子邮件。
        ```

        **对于后端更改：**
        ```
        自动化测试已通过。对于手动验证，请遵循以下步骤：

        **手动验证步骤：**
        1.  **确保服务器正在运行。**
        2.  **在终端中执行以下命令：** `curl -X POST http://localhost:8080/api/v1/users -d '{"name": "test"}'`
        3.  **确认你收到：** 状态为 `201 Created` 的 JSON 响应。
        ```

5.  **等待明确的用户反馈：**
    -   展示详细计划后，要求用户确认：“**这是否符合你的预期？请确认是 (yes) 或提供有关需要更改的反馈。**”
    -   **暂停** 并等待用户的回复。没有明确的 yes 或确认不要继续。

6.  **创建 Checkpoint Commit:**
    -   暂存所有更改。如果此步骤中未发生更改，则继续进行空提交。
    -   使用清晰简洁的消息执行提交（必须使用中文 Type，例如：`杂项: 阶段 X 结束检查点`）。

7.  **附加可审计验证报告 (Git Notes):**
    -   **步骤 7.1: 起草 Note 内容:** 创建详细的验证报告，包括自动化测试命令、手动验证步骤和用户的确认。**报告内容必须完全使用中文。**
    -   **步骤 7.2: 附加 Note:** 使用 `git notes` 命令和上一步的完整 commit hash 将完整报告附加到 checkpoint commit。

8.  **获取并记录阶段 Checkpoint SHA:**
    -   **步骤 8.1: 获取 Commit Hash:** 获取 *刚刚创建的 checkpoint commit* 的 hash (`git log -1 --format="%H"`).
    -   **步骤 8.2: 更新 Plan:** 阅读 `plan.md`，找到完成阶段的标题，并以 `[checkpoint: <sha>]` 格式追加 commit hash 的前 7 个字符。
    -   **步骤 8.3: 写入 Plan:** 将更新的内容写回 `plan.md`。

9. **提交 Plan 更新：**
    - **行动：** 暂存修改后的 `plan.md` 文件。
    - **行动：** 使用描述性消息提交此更改，例如 `杂项: 标记阶段 '<PHASE NAME>' 为完成`。

10.  **宣布完成：** 通知用户该阶段已完成，检查点已创建，详细验证报告已作为 git note 附加。

### Quality Gates (质量门禁)

在标记任何任务完成之前，请验证：

- [ ] 所有测试通过
- [ ] 代码覆盖率符合要求 (>80%)
- [ ] 代码遵循项目的代码规范（定义在 `.Docs/代码规范/` 中）
- [ ] 所有公共函数/方法均已记录文档（例如，docstrings, JSDoc, GoDoc）
- [ ] 强制执行类型安全（例如，type hints, TypeScript types, Go types）
- [ ] 无 linting 或静态分析错误（使用项目配置的工具）
- [ ] 在移动设备上正常工作（如适用）
- [ ] 文档已更新（如需要）
- [ ] 未引入安全漏洞

## Development Commands (开发命令)

**AI AGENT INSTRUCTION: 此部分应适应项目的特定语言、框架和构建工具。**

### Setup (设置)
```bash
# Example: Commands to set up the development environment (e.g., install dependencies, configure database)
# e.g., for a Node.js project: npm install
# e.g., for a Go project: go mod tidy
```

### Daily Development (日常开发)
```bash
# Example: Commands for common daily tasks (e.g., start dev server, run tests, lint, format)
# e.g., for a Node.js project: npm run dev, npm test, npm run lint
# e.g., for a Go project: go run main.go, go test ./..., go fmt ./...
```

### Before Committing (提交前)
```bash
# Example: Commands to run all pre-commit checks (e.g., format, lint, type check, run tests)
# e.g., for a Node.js project: npm run check
# e.g., for a Go project: make check (if a Makefile exists)
```

## Testing Requirements (测试要求)

### Unit Testing (单元测试)
- 每个模块必须有相应的测试。
- 使用适当的测试 setup/teardown 机制（例如，fixtures, beforeEach/afterEach）。
- Mock 外部依赖。
- 测试成功和失败的情况。

### Integration Testing (集成测试)
- 测试完整的用户流程
- 验证数据库事务
- 测试身份验证和授权
- 检查表单提交

### Mobile Testing (移动端测试)
- 尽可能在实际 iPhone 上测试
- 使用 Safari 开发者工具
- 测试触摸交互
- 验证响应式布局
- 检查 3G/4G 网络下的性能

## Code Review Process (代码审查流程)

### Self-Review Checklist (自查清单)
请求审查前：

1. **Functionality (功能性)**
   - 功能按规范工作
   - 边缘情况已处理
   - 错误消息用户友好

2. **Code Quality (代码质量)**
   - 遵循规范
   - 应用 DRY 原则
   - 变量/函数命名清晰
   - 适当的注释

3. **Testing (测试)**
   - 单元测试全面
   - 集成测试通过
   - 覆盖率充足 (>80%)

4. **Security (安全)**
   - 无硬编码密钥
   - 存在输入验证
   - 防止 SQL 注入
   - 实施 XSS 保护

5. **Performance (性能)**
   - 数据库查询优化
   - 图片优化
   - 在需要的地方实施缓存

6. **Mobile Experience (移动体验)**
   - 触摸目标充足 (44x44px)
   - 文本无需缩放即可阅读
   - 移动设备性能可接受
   - 交互感觉原生

## Commit Guidelines (提交指南)

**全局强制：所有 Commit Message 必须使用中文 Type 和中文描述。**

### Message Format (消息格式)
```
<中文类型>: <中文描述>

[可选正文]

[可选页脚]
```

### Types (中文类型映射表)
AI 在生成 Commit 时，必须严格执行以下类型转换：
- `feat`     -> **新增** (新功能)
- `fix`      -> **修复** (Bug 修复)
- `docs`     -> **文档** (仅文档变更)
- `style`    -> **格式** (不影响逻辑的代码格式变动)
- `refactor` -> **重构** (既不修复 bug 也不添加功能的代码更改)
- `perf`     -> **性能** (提高性能的代码更改)
- `test`     -> **测试** (添加缺失的测试或更正现有测试)
- `build`    -> **构建** (影响构建系统或外部依赖的更改)
- `ci`       -> **集成** (CI 配置文件和脚本的更改)
- `chore`    -> **杂项** (其他不修改 src 或 test 文件的更改)
- `revert`   -> **回滚** (撤销以前的提交)

### Examples (中文示例)
```bash
git commit -m "新增: 添加记住我功能"
git commit -m "修复: 修正短文章的摘要生成"
git commit -m "测试: 添加表情符号反应限制的测试"
git commit -m "格式: 改进按钮触摸目标区域"
git commit -m "杂项: 升级依赖包版本"
```

## Definition of Done (完成定义 - DoD)

当满足以下条件时，任务即为完成：

1. 所有代码按 Specification 实现
2. 单元测试已编写并通过
3. 代码覆盖率符合项目要求
4. 文档已完成（如适用）
5. 代码通过所有配置的 linting 和静态分析检查
6. 在移动设备上工作完美（如适用）
7. 实现说明已添加到 `plan.md`
8. 更改已使用正确的消息提交（使用中文 Type）
9. 带有任务摘要的 Git note 已附加到 commit（使用中文内容）

## Emergency Procedures (紧急程序)

### Critical Bug in Production (生产环境严重 Bug)
1. 从 main 创建 hotfix 分支
2. 为 bug 编写失败测试
3. 实现 minimal fix
4. 彻底测试，包括移动端
5. 立即部署
6. 在 plan.md 中记录

### Data Loss (数据丢失)
1. 停止所有写入操作
2. 从最新备份恢复
3. 验证数据完整性
4. 记录事故
5. 更新备份程序

### Security Breach (安全漏洞)
1. 立即轮换所有密钥
2. 审查访问日志
3. 修补漏洞
4. 通知受影响用户（如有）
5. 记录并更新安全程序

## Deployment Workflow (部署工作流)

### Pre-Deployment Checklist (部署前清单)
- [ ] 所有测试通过
- [ ] 覆盖率 >80%
- [ ] 无 linting 错误
- [ ] 移动端测试完成
- [ ] 环境变量已配置
- [ ] 数据库迁移已准备
- [ ] 备份已创建

### Deployment Steps (部署步骤)
1. 将 feature 分支合并到 main
2. 用版本标记 release
3. 推送到部署服务
4. 运行数据库迁移
5. 验证部署
6. 测试关键路径
7. 监控错误

### Post-Deployment (部署后)
1. 监控分析
2. 检查错误日志
3. 收集用户反馈
4. 规划下一次迭代