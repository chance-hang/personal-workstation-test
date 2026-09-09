# ACTIVE TASK

## 当前状态

Waiting for Prod Human Acceptance

## 当前目标

“个人工作台 Test → Prod 发布架构”阶段 B 的 Prod 三文件结构拆分已经完成、通过 ChatGPT Review，并已合并到正式库 `main`。

当前不执行新的 Test 代码任务，等待 Prod 浏览器人工验收。

## 当前架构

- Test Workspace：独立打开 `personal-workstation-test`
- Prod Workspace：独立打开 `personal-workstation-prod`
- Prod 本地 `origin` → `hb27bp49vk-source/personal-workstation`
- Prod 本地 `test` → `hb27bp49vk-source/personal-workstation-test`

## 当前要求

Codex 如果在 Test Workspace 读取本文件：

- 不创建新分支
- 不修改 Test 业务代码
- 不执行 Test → Prod 发布
- 保持 Test `main` 稳定

## 下一步

Prod 人工验收通过后，由 ChatGPT 进入阶段 C：

- 固化 Test → Prod 发布清单
- 明确 Release Ready 状态
- 固化 Prod 通过 `test` remote 获取指定 Test commit 的发布方式
- 建立发布历史记录
