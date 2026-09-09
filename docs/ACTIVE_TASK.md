# ACTIVE TASK

## 当前状态

Active

## 当前目标

执行项目结构优化阶段 1：

`index.html → index.html + styles.css + app.js`

## 对应 Plan

`docs/plans/2026-09-09-split-single-file-architecture.md`

## 当前阶段

阶段 1 — 机械拆分

## 当前分支

`codex/split-single-file-phase-1`

## 执行要求

Codex 开始前：

1. 读取 `AGENTS.md`。
2. 读取本文件。
3. 完整读取对应 Plan 的“阶段 1”与验证要求。
4. 确认当前仓库为 `hb27bp49vk-source/personal-workstation-test`。
5. `git fetch`。
6. 从最新 `main` 同步后创建/切换到：
   `codex/split-single-file-phase-1`
7. 若工作区存在未提交修改，停止并汇报，不要自动清理或覆盖。

本轮只做：

- 将主要 CSS 从 `index.html` 迁移到根目录 `styles.css`
- 将主要 JavaScript 从 `index.html` 迁移到根目录 `app.js`
- 在 `index.html` 中正确引用它们
- 做等价性验证

本轮禁止：

- 业务功能新增
- UI 重设计
- 数据结构修改
- localStorage 协议修改
- GitHub Gist 同步协议修改
- JS 业务模块化拆分
- 引入 npm / 构建工具 / 框架
- 无关重构或全局格式化
- 执行原打卡 Plan 的 Task 3–6

## 完成后

完成并验证后：

1. 检查 `git diff`，确认只有本阶段相关修改。
2. commit 当前任务分支。
3. 提交信息：
   `refactor: 拆分单文件为 HTML CSS JS`
4. push 当前任务分支到 GitHub。
5. 不合并 `main`。
6. 停止等待 ChatGPT Review。

## 汇报要求

不要长篇复述 Plan，只需用中文汇报：

- 是否拆分成功
- 生成了哪些文件
- 是否做了业务逻辑修改
- localStorage / Gist 是否有协议变化
- 做了哪些验证
- 哪些验证因为环境限制无法完成
- commit SHA
- push 是否成功
- 当前分支
- 工作区是否干净
