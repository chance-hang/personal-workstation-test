# ACTIVE TASK

## 当前状态

Waiting for Prod execution

## 当前目标

继续“个人工作台 Test → Prod 发布架构”阶段 B：

**Prod 单文件结构机械拆分**

## 执行入口已调整

由于本机 Codex 对父目录多仓库 Workspace 初始化不稳定，阶段 B 不再要求在同一个 Workspace 同时打开 Test 与 Prod。

现在采用：

- Test Workspace：独立打开 `personal-workstation-test`
- Prod Workspace：独立打开 `personal-workstation-prod`
- Prod 本地 Git 配置 `test` remote 指向 `hb27bp49vk-source/personal-workstation-test`

阶段 B 的实际执行任务已经放到正式仓库：

`hb27bp49vk-source/personal-workstation/docs/ACTIVE_TASK.md`

## 当前要求

Test 仓库本轮不再执行任何业务修改。

Codex 如果在 Test Workspace 读取本文件：

- 不创建新分支
- 不修改 Test 业务代码
- 不继续执行旧版阶段 B 指令
- 保持 Test `main` 稳定

正式结构拆分请切换到 Prod Workspace，并读取 Prod 仓库自己的：

- `AGENTS.md`
- `docs/ACTIVE_TASK.md`

## 长期工作流方向

后续采用：

Test 开发 → ChatGPT Review → 人工验收 → 标记 Release Ready → Prod Workspace 通过 `test` remote 获取指定 Test 版本 → 执行受控发布。
