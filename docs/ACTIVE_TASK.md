# ACTIVE TASK

## 当前状态

Active

## 当前目标

执行“个人工作台 Test → Prod 发布架构”阶段 A：

**差异审计 + 环境配置方案落地**

## 对应 Plan

`docs/plans/2026-09-09-test-prod-release-architecture.md`

## 当前分支

`codex/test-prod-release-audit`

## 当前仓库

`hb27bp49vk-source/personal-workstation-test`

## 对应正式仓库

`hb27bp49vk-source/personal-workstation`

## 本轮目标

先确认 Test / Prod 的真实代码差异，特别是正式环境专属行为，再决定如何把环境差异从业务代码中隔离出来。

本轮仍以 Test 仓库为工作区，不修改正式仓库。

## 开始前

1. 读取 `AGENTS.md`。
2. 读取本文件。
3. 完整读取对应 Plan 的“阶段 A”。
4. `git fetch`。
5. 确认当前仓库是 `personal-workstation-test`。
6. 同步最新 `main`。
7. 从最新 `main` 创建/切换到 `codex/test-prod-release-audit`。
8. 如果工作区不干净，停止并汇报，不自动清理。

## 本轮只做

### A1. Test / Prod 差异审计

允许读取 GitHub 上的正式仓库 `hb27bp49vk-source/personal-workstation` 进行对比，但禁止向正式仓库写入。

重点确认：

- Prod 单文件 `index.html` 中哪些 CSS / JS 对应 Test 当前 `styles.css` / `app.js`。
- 正式版是否存在 Test 没有的专属登录逻辑。
- 刷新后的 Chance 登录提示与默认登录行为。
- localStorage 数据结构和关键字段是否一致。
- GitHub Gist 加密同步路径是否一致。
- 导出 / 导入行为是否一致。
- 页面初始化顺序是否存在差异。
- 是否存在正式版独有文案、开关或保护逻辑。

把差异分类为：

1. 应继续保留的生产环境差异。
2. 已过时、无需保留的历史差异。
3. 可抽取成环境配置的差异。
4. 暂时无法安全判断的差异。

### A2. 环境配置方案

如果审计结果支持安全落地，可在当前 Test 分支中新增最小 `env.js` 或等价环境配置层。

目标是让：

- `index.html`
- `styles.css`
- `app.js`

以后尽量可以作为 Test / Prod 共享业务代码；环境差异由独立配置承载。

如果实际代码不适合 `env.js`，不要硬做，先把替代方案写清楚并停止在文档阶段。

### A3. 文档回写

在当前分支增加一份差异审计结果文档：

`docs/test-prod-diff-audit.md`

至少记录：

- Test / Prod 当前结构
- 关键差异
- 环境差异清单
- 推荐迁移方案
- Prod 迁移风险
- 阶段 B 前置条件

## 本轮禁止

- 不修改 `hb27bp49vk-source/personal-workstation` 正式仓库。
- 不执行 Test → Prod 发布。
- 不复制 Test 文件覆盖 Prod。
- 不重新拆分 `app.js`。
- 不引入 npm / 构建工具 / 框架。
- 不改变 localStorage 核心字段。
- 不改变 GitHub Gist 加密同步协议。
- 不做无关 UI / 业务重构。
- 不全局格式化。

## 验证

如果只完成审计文档：

- 确认文档能明确解释 Prod 专属行为和迁移风险。

如果同时新增环境配置层：

至少验证：

1. Test 浏览器直接运行正常。
2. 页面主要 Tab 正常。
3. 登录行为与改造前 Test 一致。
4. localStorage 数据可正常读取。
5. Gist 同步路径未改变。
6. 导入 / 导出路径未改变。
7. 页面刷新和初始化正常。

## 完成后

1. 检查 `git diff`。
2. commit 当前分支。
3. 推荐提交信息：`chore: 审计 Test Prod 差异并设计环境配置`
4. push `codex/test-prod-release-audit`。
5. 不合并 `main`。
6. 不修改 Prod。
7. 停止等待 ChatGPT Review。

## 汇报要求

用中文汇报：

- 是否完成差异审计
- 是否新增环境配置层
- Prod 有哪些必须保留的专属差异
- localStorage / Gist / 导入导出是否存在差异
- 修改了哪些 Test 文件
- 做了哪些验证
- 哪些地方仍无法确定
- commit SHA
- push 是否成功
- 当前分支
