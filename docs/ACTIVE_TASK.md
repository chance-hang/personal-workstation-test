# ACTIVE TASK

## 当前状态

Completed

## 当前目标

个人工作台 Test → Prod 基础发布架构已经建立：

- Test / Prod 差异审计完成
- Prod 已完成三文件结构迁移
- Prod 已通过 ChatGPT Review 和人工验收
- Prod 已建立独立 `AGENTS.md`、`docs/ACTIVE_TASK.md`、`docs/RELEASE.md`、`docs/RELEASE_HISTORY.md`
- Prod 本地通过 `test` remote 读取 Test

当前没有待执行的 Test Codex 任务。

## 长期开发流程

Test 是唯一常规开发入口。

以后每个功能：

用户需求 → ChatGPT Plan / ACTIVE_TASK → Codex 在 Test 开发 → push → ChatGPT Review → 用户人工验收 → ChatGPT 更新 `docs/RELEASE.md` 为 `Release Ready` → 切换 Prod Workspace 执行受控发布。

## 当前要求

Codex 读取本文件后，如果没有新的 ChatGPT 指令：

- 不创建新分支
- 不修改业务代码
- 不执行历史 Plan
- 不主动发布到 Prod
- 保持 `main` 为当前稳定 Test 基线

下一次新需求开始时，由 ChatGPT 更新本文件。
