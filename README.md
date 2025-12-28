# Gemini CLI 的 DWorkflow 扩展 (DWorkflow Extension)

**三思而后行，一次把代码写对。**

DWorkflow 是一个 Gemini CLI 扩展，旨在实现 **上下文驱动开发 (Context-Driven Development)**。它将 Gemini CLI 转变为一个主动的项目经理，遵循严格的协议来制定规范、规划并实现软件功能和 Bug 修复。

DWorkflow 不仅仅是写代码，它确保每个任务都拥有连贯、高质量的生命周期：**Context (上下文) -> Spec (规格) -> Plan (计划) -> Implement (实现)**。

DWorkflow 背后的理念很简单：掌控你的代码。通过将上下文视为与代码并存的受管工件，你将代码库转变为单一事实来源 (Single Source of Truth)，从而以深度、持久的项目感知能力驱动每一次 AI 智能体交互。

## Features (特性)

-   **Plan before you build (谋定而后动)**：为新代码库和现有代码库创建指导智能体的 Spec (规格) 和 Plan (计划)。
-   **Maintain context (保持上下文)**：确保 AI 遵循风格指南、技术栈选择和产品目标。
-   **Iterate safely (安全迭代)**：在编写代码之前审查计划，让你牢牢掌握控制权。
-   **Work as a team (团队协作)**：为你的产品、技术栈和工作流偏好设置项目级上下文，使其成为团队的共享基础。
-   **Build on existing projects (基于现有项目构建)**：针对新项目 (Greenfield) 和现有项目 (Brownfield) 的智能初始化。
-   **Smart revert (智能回滚)**：Git 感知的回滚命令，理解工作逻辑单元（Track, Phase, Task）而不仅仅是 Commit Hash。

## Installation (安装)

在终端运行以下命令安装 DWorkflow 扩展：

```bash
gemini extensions install https://github.com/gemini-cli-extensions/DWorkflow --auto-update
```

`--auto-update` 是可选的：如果指定，它将在新版本发布时自动更新。

## Usage (使用方法)

DWorkflow 旨在管理开发任务的整个生命周期。

**关于 Token 消耗的说明：** DWorkflow 的上下文驱动方法涉及阅读和分析项目的上下文、规格和计划。这可能会导致 Token 消耗增加，特别是在大型项目或广泛的规划和实施阶段。你可以通过运行 `/stats model` 来查看当前会话的 Token 消耗。

### 1. Set Up the Project (项目设置 - 仅需运行一次)

运行 `/DW:setup` 时，DWorkflow 会帮助你定义项目上下文的核心组件。此上下文随后将由你或你团队中的任何人用于构建新组件或功能。

-   **Product (产品)**：定义项目上下文（例如用户、产品目标、高级功能）。
-   **Product guidelines (产品指南)**：定义标准（例如文案风格、品牌信息、视觉识别）。
-   **Tech stack (技术栈)**：配置技术偏好（例如语言、数据库、框架）。
-   **Workflow (工作流)**：设置团队偏好（例如 TDD、提交策略）。使用 [workflow.md](templates/workflow.md) 作为可自定义的模板。

**生成的工件 (Artifacts)：**
-   `DWorkflow/product.md`
-   `DWorkflow/product-guidelines.md`
-   `DWorkflow/tech-stack.md`
-   `DWorkflow/workflow.md`
-   `DWorkflow/code_styleguides/`
-   `DWorkflow/tracks.md`

```bash
/DW:setup
```

### 2. Start a New Track (启动新轨道 - Feature 或 Bug)

当你准备好处理新功能或 Bug 修复时，运行 `/DW:newTrack`。这将初始化一个 **Track (轨道)** —— 一个高层级的工作单元。DWorkflow 帮助你生成两个关键工件：

-   **Specs (规格)**：特定工作的详细需求。我们要构建什么？为什么？
-   **Plan (计划)**：包含 Phase (阶段)、Task (任务) 和 Sub-task (子任务) 的可操作待办事项列表。

**生成的工件：**
-   `DWorkflow/tracks/<track_id>/spec.md`
-   `DWorkflow/tracks/<track_id>/plan.md`
-   `DWorkflow/tracks/<track_id>/metadata.json`

```bash
/DW:newTrack
# 或者带描述
/DW:newTrack "Add a dark mode toggle to the settings page"
```

### 3. Implement the Track (实现轨道)

批准计划后，运行 `/DW:implement`。你的编码智能体随后将按照 `plan.md` 文件工作，在完成任务时将其勾选。

**更新的工件：**
-   `DWorkflow/tracks.md` (状态更新)
-   `DWorkflow/tracks/<track_id>/plan.md` (状态更新)
-   项目上下文文件 (完成后同步)

```bash
/DW:implement
```

DWorkflow 将：
1.  选择下一个待处理的任务。
2.  遵循定义的工作流（例如，TDD：编写测试 -> 失败 -> 实现 -> 通过）。
3.  随着进度更新计划中的状态。
4.  **Verify Progress (验证进度)**：在每个阶段结束时引导你进行手动验证步骤，以确保一切按预期工作。

在实现过程中，你还可以：

-   **Check status (检查状态)**：获取项目进度的概览。
    ```bash
    /DW:status
    ```
-   **Revert work (回滚工作)**：如果需要，撤销功能或特定任务。
    ```bash
    /DW:revert
    ```

## Commands Reference (命令参考)

| Command | Description (描述) | Artifacts (工件) |
| :--- | :--- | :--- |
| `/DW:setup` | 搭建项目脚手架并设置 DWorkflow 环境。每个项目运行一次。 | `DWorkflow/product.md`<br>`DWorkflow/product-guidelines.md`<br>`DWorkflow/tech-stack.md`<br>`DWorkflow/workflow.md`<br>`DWorkflow/tracks.md` |
| `/DW:newTrack` | 启动新的 Feature 或 Bug Track。生成 `spec.md` 和 `plan.md`。 | `DWorkflow/tracks/<id>/spec.md`<br>`DWorkflow/tracks/<id>/plan.md`<br>`DWorkflow/tracks.md` |
| `/DW:implement` | 执行当前 Track 的 Plan 中定义的任务。 | `DWorkflow/tracks.md`<br>`DWorkflow/tracks/<id>/plan.md` |
| `/DW:status` | 显示 Tracks 文件和活动 Tracks 的当前进度。 | 读取 `DWorkflow/tracks.md` |
| `/DW:revert` | 通过分析 git 历史记录回滚 Track, Phase, 或 Task。 | 回滚 git 历史 |

## Resources (资源)

-   [Gemini CLI extensions](https://geminicli.com/docs/extensions/): 关于在 Gemini CLI 中使用扩展的文档
-   [GitHub issues](https://github.com/gemini-cli-extensions/DWorkflow/issues): 报告 Bug 或请求功能

## Legal (法律信息)

-   License: [Apache License 2.0](LICENSE)
