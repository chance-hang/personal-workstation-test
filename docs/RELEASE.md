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

当前仍处于 Test → Prod 发布架构治理阶段。

在完成差异审计、环境配置隔离和 Prod 结构迁移之前，不执行正式发布。

## 发布原则

- 常规开发只在 Test 进行。
- Prod 不重新实现 Test 已完成的功能。
- 只有经过 ChatGPT Review 和人工验收的 Test commit 才可成为发布候选。
- 发布前必须记录 Source commit。
- 环境专属文件或配置不得被跨环境无脑覆盖。
- 任何正式发布前必须重新检查 Prod 当前状态，避免覆盖正式环境独有修改。

## 当前发布候选

无。

## 下一步

执行：

`docs/plans/2026-09-09-test-prod-release-architecture.md`

阶段 A：差异审计与方案落地。
