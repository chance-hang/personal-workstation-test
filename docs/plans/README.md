# Implementation Plans

本目录用于存放由 ChatGPT 规划、交给 Codex 执行的具体开发任务。

目标：让需求分析、方案设计和代码执行分离，减少 Codex 在大型 `index.html` 中重复探索和重新规划所消耗的上下文，同时让多台电脑上的 Codex 可以通过 GitHub 共享同一套任务状态。

## 基本原则

1. 复杂需求先规划，再编码。
2. 一个 Plan 对应一个明确的功能、Bug 或重构目标。
3. Plan 应尽量指出相关代码区域、函数、DOM id、数据结构等定位信息，减少 Codex 全量读取 `index.html`。
4. Codex 一次只执行 Plan 中明确指定的 Task，不默认执行整个 Plan。
5. Task 有依赖关系时必须按顺序执行；只有明确标记可并行的 Task 才允许多台电脑同时处理。
6. 每个并行任务使用独立 Git 分支，不允许多台电脑同时直接修改 `main`。
7. 执行过程中发现计划外问题时先记录和汇报，不自行扩大修改范围。
8. Plan 是任务说明，不代替 `AGENTS.md`；所有任务仍必须遵守仓库根目录的 `AGENTS.md`。

## 文件命名

建议格式：

`YYYY-MM-DD-short-task-name.md`

例如：

- `2026-09-08-money-account-filter.md`
- `2026-09-08-fix-mobile-nav.md`
- `2026-09-09-habit-checkin-improvement.md`

不要长期维护一个多人共用的 `current.md`，以免多台电脑同时工作时发生覆盖或状态混乱。

## Plan 模板

```markdown
# 任务名称

## 状态

Planned / In Progress / Blocked / Completed

## 目标

说明最终希望实现什么，以及用户能够观察到的结果。

## 当前问题

说明现有行为、限制或 Bug。

## 相关代码区域

尽可能提供定位信息，例如：

- 文件：`index.html`
- 模块/注释标题：
- 相关函数：
- DOM id / class / data-module：
- localStorage / 状态字段：

避免要求 Codex 为了寻找入口而反复读取整个文件。

## 实现方案

描述已经确定的实现方向和关键决策。

这里应解决“怎么做”的主要决策，让 Codex 重点负责执行，而不是重新进行完整架构设计。

## 不允许修改的范围

明确本任务不应该改变的内容，例如：

- 不修改其他模块
- 不改变现有数据格式
- 不进行全局格式化
- 不拆分 `index.html`
- 不修改 GitHub Gist 同步协议

根据任务实际情况填写。

## Tasks

### Task 1 — 任务名称

状态：Pending

依赖：无

建议分支：`codex/example-task-1`

修改范围：
- ...

要求：
- ...

验证：
- ...

### Task 2 — 任务名称

状态：Pending

依赖：Task 1

建议分支：`codex/example-task-2`

修改范围：
- ...

要求：
- ...

验证：
- ...

## 并行执行说明

明确说明哪些 Task 可以并行，哪些必须等待前置 Task 完成。

例如：

- Task 1 必须先完成。
- Task 2 和 Task 3 在 Task 1 合并后可以并行。
- Task 4 必须等待 Task 2、Task 3 合并后执行。

## 验证方法

列出整体功能验证步骤，包括必要的桌面端、移动端、本地存储、Gist 同步或数据兼容性检查。

## 完成标准

明确什么情况下这个 Plan 可以标记为 Completed。

## Codex 完成后必须汇报

- 实际修改的文件/代码区域
- 实际修改的函数
- 是否改变数据结构
- 是否影响 localStorage
- 是否影响 GitHub Gist 同步
- 执行了哪些验证
- 验证结果
- 是否发现计划外但未处理的问题
```

## 推荐的 ChatGPT → Codex 流程

用户先和 ChatGPT 讨论需求。ChatGPT 阅读必要的仓库代码并生成本目录下的 Plan。

随后只给 Codex 一个短而明确的执行指令，例如：

`Implement Task 1 from docs/plans/2026-09-08-money-account-filter.md. Follow AGENTS.md. Do not execute other tasks.`

Codex 完成后提交代码并汇报结果，再由用户或 ChatGPT 检查结果并决定是否开始下一个 Task。

## 多电脑工作方式

每台电脑开始任务前应先同步 GitHub，并确认自己负责的 Task 和分支。

推荐：

- 电脑 A → Task 1 → `codex/task-1`
- 电脑 B → Task 2 → `codex/task-2`
- 电脑 C → Task 3 → `codex/task-3`

只有当 Plan 明确说明 Task 可以并行时才这样做。如果多个 Task 会修改 `index.html` 中高度重叠的区域，优先串行执行，以减少合并冲突。
