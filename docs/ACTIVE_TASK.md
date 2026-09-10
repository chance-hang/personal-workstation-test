# ACTIVE TASK

最后更新：2026-09-10（Workflow 3.0 Phase 2 同步）

## 当前状态

`Completed / Accepted`

- Test → Prod 基础发布架构已经建立；
- Test / Prod 差异审计完成；
- Prod 已完成三文件结构迁移；
- Prod 已通过 ChatGPT Review 和人工验收；
- Prod 已建立独立 `AGENTS.md`、`docs/ACTIVE_TASK.md`、`docs/RELEASE.md`、`docs/RELEASE_HISTORY.md`；
- Prod 本地通过 `test` remote 读取 Test。

当前没有待执行的 Test Codex 任务。

## 当前优先级

- 没有 P0 Active。
- 没有 P1 Queued。
- `P2 Backlog`：等待 ChatGPT 派发新需求；新需求到达前 Codex 不主动实施任何变更。

## STOP 状态机

当 Codex 开始一次新任务时，必须按 `GLOBAL_RULES.md §10` 报告 STOP 状态：

- `Awaiting ChatGPT Review`：commit / push 完成后等 ChatGPT Review diff。
- `Awaiting User Acceptance`：Review 通过后等用户人工验收。
- `Blocked`：缺信息 / 冲突 / 依赖未到位。
- `Completed / Accepted`：用户人工验收通过，ChatGPT 派发下一 Task 或执行发布。

到达 `Awaiting ChatGPT Review` / `Awaiting User Acceptance` 时，Codex 必须 STOP，不得自行一路推进到 Prod。

## 长期开发流程

Test 是唯一常规开发入口。

以后每个功能：

用户需求 → ChatGPT Plan / ACTIVE_TASK（P0 Active）→ Codex 在 Test 开发 → push → `Awaiting ChatGPT Review` → ChatGPT Review → `Awaiting User Acceptance` → 用户人工验收 → `Completed / Accepted` → ChatGPT 更新 `docs/RELEASE.md` 为 `Release Ready` → 切换 Prod Workspace 执行受控发布。

## 当前要求

Codex 读取本文件后，如果没有新的 ChatGPT 指令：

- 不创建新分支
- 不修改业务代码
- 不执行历史 Plan
- 不主动发布到 Prod
- 不把 P2 Backlog 自行提升为 P0
- 保持 `main` 为当前稳定 Test 基线

下一次新需求开始时，由 ChatGPT 更新本文件并把对应任务升为 `P0 Active`。