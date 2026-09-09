# RELEASE

## 当前状态

Not Ready

## 项目

个人工作台

## Source

`hb27bp49vk-source/personal-workstation-test`

## Target

`hb27bp49vk-source/personal-workstation`

## 当前说明

阶段 A（Test / Prod 差异审计）已完成并通过 ChatGPT Review。

当前进入阶段 B：Prod 结构迁移。

本阶段只把 Prod 现有单文件结构机械拆分为：

- `index.html`
- `styles.css`
- `app.js`

不把 Test 业务代码直接覆盖到 Prod，不执行功能发布，不新增 `env.js`。

## 发布原则

- 常规开发只在 Test 进行。
- Prod 不重新实现 Test 已完成的功能。
- 只有经过 ChatGPT Review 和人工验收的 Test commit 才可成为发布候选。
- 发布前必须记录 Source commit。
- 环境专属文件或配置不得被跨环境无脑覆盖。
- 任何正式发布前必须重新检查 Prod 当前状态，避免覆盖正式环境独有修改。

## 当前发布候选

无。

## 当前阶段

执行：

`docs/plans/2026-09-09-test-prod-release-architecture.md`

阶段 B：Prod 结构迁移。

阶段 B 完成并通过 Review / 浏览器回归后，再进入阶段 C：发布流程固化。
