# 个人工作台 Test → Prod 发布架构计划

## 状态

Completed

## 背景

当前存在两个独立仓库：

- Test：`chance-hang/personal-workstation-test`
- Prod：`chance-hang/personal-workstation`

本计划用于把原先彼此独立、结构不一致的 Test / Prod，改造成可重复执行的开发与发布体系。

## 已完成结果

### 1. Test / Prod 差异审计

已完成正式版与测试版的结构、登录、localStorage、IndexedDB、Gist、导入导出和初始化差异审计。

结论：环境差异不能通过无脑覆盖处理，正式版行为必须在发布时被显式保护。

### 2. Prod 三文件结构迁移

Prod 已从单文件 `index.html` 机械拆分为：

- `index.html`
- `styles.css`
- `app.js`

结构拆分没有同步 Test 新功能，已通过 ChatGPT Review，并完成用户人工验收。

关键结构迁移提交：

`2361b340527e186b210fbb549ba7a465ff2b5dd6`

### 3. 独立 Workspace + Git remote 架构

由于本机 Codex 对父目录多仓库 Workspace 初始化不稳定，最终采用四个独立 Git Workspace。

个人工作台：

- Test Workspace：`personal-workstation-test`
- Prod Workspace：`personal-workstation-prod`

Prod 本地 Git 约定：

- `origin` → `chance-hang/personal-workstation`
- `test` → `chance-hang/personal-workstation-test`

Prod 通过 `git fetch test` 获取经过验收的 Test commit，不依赖跨目录 Workspace。

### 4. Test → Prod 发布协议

Test 负责：

用户需求 → ChatGPT Plan / ACTIVE_TASK → Codex 开发 → push → ChatGPT Review → 用户人工验收 → `docs/RELEASE.md` 标记 `Release Ready`。

Prod 负责：

读取自己的 `AGENTS.md`、`docs/ACTIVE_TASK.md`、`docs/RELEASE.md` → `git fetch test` → 获取指定 Source Test commit → 在独立发布分支中做受控同步 → push → ChatGPT Review → 合并 → 用户人工验收。

禁止：

- 直接 `git merge test/main`
- 整库覆盖 Prod
- 在 Prod 独立重新实现 Test 已完成的需求
- 无视 Prod 正式环境行为进行文件覆盖

### 5. 发布历史

Prod 已建立：

`docs/RELEASE_HISTORY.md`

用于记录每次正式发布的：

- Source Test commit
- Prod 发布提交
- 发布范围
- 验收结果
- 回滚信息

## 长期规则

1. 常规开发只在 Test。
2. Prod 只作为正式发布区。
3. Test 通过 ChatGPT Review 和人工验收后才可成为发布候选。
4. 每次发布必须有明确 Source Test commit 与允许修改范围。
5. Prod 环境差异必须被显式保护。
6. 发布必须经过独立发布分支、ChatGPT Review 和人工验收。
7. GitHub 是两台电脑和多个 Workspace 之间的共享状态来源。

## 关于 env.js

本计划最初考虑使用 `env.js` 统一环境差异。

经过差异审计后，决定不把 `env.js` 作为本轮架构完成的强制条件。当前先通过明确的发布清单和 Prod 行为保护规则管理环境差异。

如果以后 Test / Prod 业务代码继续趋同、且实际发布成本证明有必要，可单独立项做最小环境配置层；不得与普通功能发布顺便混做。

## 完成标准

本计划已完成：

- Test / Prod 结构差异已审计
- Prod 三文件结构迁移并人工验收通过
- Test / Prod 独立 Workspace 方案确定
- Prod `test` remote 方案确定并验证
- Test Release 清单规则建立
- Prod Release 执行规则建立
- Prod 发布历史建立
- Test 与 Prod 日常职责边界明确

后续不再继续本 Plan。新的产品需求使用新的 Plan；新的 Test → Prod 发布由当次 `docs/RELEASE.md` 和 Prod `docs/ACTIVE_TASK.md` 驱动。
