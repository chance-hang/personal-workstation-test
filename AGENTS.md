# AGENTS.md

## 项目说明

这是“个人工作台”的测试版，也是常规功能开发、重构、Bug 修复和验收的唯一开发入口。

对应正式仓库：

`chance-hang/personal-workstation`

当前应用采用浏览器直接运行、无构建步骤、无 npm / Node.js 依赖的轻量结构。
数据主要存储于 localStorage，并支持 GitHub Gist 加密同步。

当前项目结构基线：
- `index.html`：HTML 页面结构
- `styles.css`：主要样式
- `app.js`：主要 JavaScript 业务逻辑

项目历史上曾采用单文件 `index.html` 架构，但已完成第一阶段机械拆分。
除非当前 `docs/ACTIVE_TASK.md` 或对应 Plan 明确授权，不要继续做新的文件拆分、模块化、框架迁移或构建系统改造。

## Test → Prod 长期规则

GitHub 中存在独立 Test / Prod 两个仓库。

长期原则：

1. 常规功能开发只在 `personal-workstation-test` 进行。
2. Test 中的功能必须先完成 ChatGPT Review 和必要的人工验收。
3. 只有已验证版本才能进入 Prod。
4. 不要在 Prod 中重新实现 Test 已经完成的功能。
5. Prod 原则上只接收 Test 已验证代码和明确的环境差异配置。
6. 发布前读取 `docs/RELEASE.md` 和当前发布 Plan。
7. 环境专属配置不得被跨环境无脑覆盖。
8. 正式仓库如存在独有修改，发布前必须重新比较并停止自动覆盖。

当前 Test / Prod 的结构仍在治理中。以：

`docs/plans/2026-09-09-test-prod-release-architecture.md`

为当前发布架构基线。

在该计划明确进入 Prod 迁移阶段之前，Codex 不得修改正式仓库。

## Codex 工作原则

### 1. 先理解任务，再读取代码

开始前优先读取：
1. `AGENTS.md`
2. `docs/ACTIVE_TASK.md`（如果存在）
3. ACTIVE_TASK 指向的 Plan

不要为了“全面理解项目”而默认读取整个大文件。

优先：
- 根据任务定位相关模块
- 搜索函数名、DOM id、`data-module`、注释标题
- HTML 结构问题优先看 `index.html`
- 样式问题优先看 `styles.css`
- 业务逻辑问题优先看 `app.js`
- 只读取相关区域及必要上下文

避免重复全量读取 `index.html`、`styles.css`、`app.js`。

### 2. 严格控制修改范围

每个任务只修改与任务直接相关的代码。

禁止：
- 顺便重构其他模块
- 全局格式化
- 大规模改名
- 改变无关 CSS
- 修改无关业务逻辑
- 因为当前已经拆成三个文件，就主动继续模块化

如果发现额外问题，记录并汇报，不要自行扩大任务范围。

### 3. 保持现有技术路线

除非当前任务计划明确要求：
- 不引入 React / Vue / Angular
- 不引入 npm 构建系统
- 不增加后端
- 不更换存储方案
- 不改变 GitHub Gist 加密同步协议
- 不改用 ES Module 或其他新的模块加载体系

新的文件拆分、目录重构或 JS 模块化只有在 ACTIVE_TASK / Plan 明确授权时才能进行。

## 多电脑协作规则

GitHub 是唯一共享状态。

任何一台电脑开始 Codex 任务之前：
1. 检查当前分支
2. `git fetch`
3. 同步最新 `main`
4. 为当前任务使用独立分支

分支示例：
- `codex/fix-habit-checkin`
- `codex/add-budget-filter`
- `codex/fix-mobile-nav`

不同电脑不得同时修改同一个任务分支。

不要让多台电脑同时直接修改 `main`。

## 任务计划

复杂任务必须先有计划。

计划文件位于：

`docs/plans/`

当前要执行什么，以：

`docs/ACTIVE_TASK.md`

为入口。

Codex 应优先执行 ACTIVE_TASK 指向的明确阶段，而不是自行重新设计整个方案。

当旧 Plan 描述的项目结构与当前基线不同，以 `AGENTS.md` 和较新的续作/迁移 Plan 为准；产品需求仍可参考原 Plan。

## 完成任务时

Codex 必须汇报：
- 修改了哪些区域
- 修改了哪些函数/文件
- 是否改变数据结构
- 是否涉及 localStorage
- 是否涉及 GitHub Gist 同步
- 如何验证
- 是否发现但未处理的其他问题

如果 ACTIVE_TASK 明确要求完成后 commit/push，则按其要求执行；否则不要擅自合并 `main`。

不要在没有说明的情况下修改数据兼容性。

## Workflow 3.0 跨项目同步（2026-09-10）

本节把总控仓库 [`chance-hang/AI-Coding-Control-Center`](https://github.com/chance-hang/AI-Coding-Control-Center) 的跨项目规则同步到本仓库。它不替代本仓库已有规则；与既有规则冲突时，以总控仓库 `GLOBAL_RULES.md §19` 恢复权威顺序为准。

权威来源（详细定义）：

- [GLOBAL_RULES.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/GLOBAL_RULES.md)
- [docs/WORKFLOW.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/WORKFLOW.md)
- [docs/EXECUTOR_HANDOFF.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/EXECUTOR_HANDOFF.md)
- [docs/MULTI_DEVICE.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/MULTI_DEVICE.md)
- [docs/DISASTER_RECOVERY.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/DISASTER_RECOVERY.md)

### 角色与执行器抽象

- 用户：提出需求、确定优先级、批准高风险操作、执行关键人工验收。
- ChatGPT：总控。读取 GitHub 事实、分析需求、设计方案、维护治理文件、Review Executor 推送结果、控制发布节奏。
- Executor：在真实本地仓库中执行明确任务的工程层。**Codex 与 Workbuddy 都是可替换 Executor**，未来如出现新的执行器按相同协议接入。
- GitHub：代码、规则、任务状态、发布记录的长期共享真源，**对 Executor 中立**。

本节"Codex 工作原则"中的 Codex 一律视作 Executor 之一。Codex 不得把本仓库状态绑定到 Codex 会话。

### ACTIVE_TASK / Task Queue 优先级模型

本仓库 `docs/ACTIVE_TASK.md` 必须为每条任务标注优先级：

| 优先级 | 含义 | Executor 允许行为 |
| --- | --- | --- |
| `P0 Active` | 当前唯一允许实施的任务 | Implementation、测试、commit、push |
| `P1 Queued` | 下一任务 | 读取、规划、写文档；**不得提前 Implementation** |
| `P2 Backlog` | 未来任务 | 不主动执行；仅在 ChatGPT 显式升级后才进入 P1 / P0 |

Codex 不得自行把 P1 / P2 提升为 P0。任何"顺手做一下"必须先升级为 P0 再开始。

### STOP 状态机

Codex 到达以下任一门槛必须立即 STOP，不得自行一路推进到 Prod：

| 状态 | 后续推进必须由谁激活 |
| --- | --- |
| `Awaiting ChatGPT Review` | ChatGPT |
| `Awaiting User Acceptance` | 用户 |
| `Blocked` | ChatGPT + 用户 |
| `Completed / Accepted` | ChatGPT 派发下一 Task 或执行发布 |

### 上下文高效指令与汇报

- ChatGPT → Codex 默认指令只给三件事：仓库绝对路径、动作（`clean-handoff-and-execute` / `execute` / `takeover-only` / `protect-then-report`）、读取入口（`AGENTS.md` / `docs/ACTIVE_TASK.md` / Plan）。
- Codex 默认完成汇报只四件事：`commit SHA` / 测试验证 / `push 成功/失败` / `blocker`。
- 仅当新需求尚未进入 GitHub、高风险操作、异常恢复、需要用户决策时才展开长指令。

### 多电脑 / Executor 接管

- 每台电脑使用独立 Git clone；GitHub 负责跨设备同步。
- 同一个仓库同一时间只能有一个写入 Executor；Codex 不同会话之间不得并行写入。
- dirty worktree 接管必须先保护前一执行器遗留工作；禁止直接 `reset --hard` / `clean -fd` / `checkout --`。
- 跨项目规则见 [docs/MULTI_DEVICE.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/MULTI_DEVICE.md) 与 [docs/EXECUTOR_HANDOFF.md](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/EXECUTOR_HANDOFF.md)。

### 云同步盘与 `.git` 风险

- 百度同步盘**不能视为 Git 状态同步机制**；GitHub 才是跨设备同步真源。
- 不得让两个 Executor / 设备同时写同一 clone。
- 遇到 ref 异常先停止、检查 `git reflog` 与 `git fsck`，**不得** reset / clean / 重写历史。详细恢复流程见 [docs/DISASTER_RECOVERY.md §场景 E](https://github.com/chance-hang/AI-Coding-Control-Center/blob/main/docs/DISASTER_RECOVERY.md)。

### 与本仓库既有规则的关系

- 既有"Test → Prod 长期规则"、"Codex 工作原则"、"多电脑协作规则"、"任务计划"等仍然有效。
- 本节只在不冲突的范围内补充跨项目同步要求；冲突时按权威顺序由 ChatGPT 显式裁决，并在 `docs/ACTIVE_TASK.md` 标注。
