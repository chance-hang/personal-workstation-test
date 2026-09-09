# RELEASE

## 当前状态

Idle

当前没有待发布版本。

## 项目

个人工作台

## Source

`hb27bp49vk-source/personal-workstation-test`

## Target

`hb27bp49vk-source/personal-workstation`

## 长期发布规则

Test 是唯一常规开发入口。

只有当某个 Test 版本同时满足：

1. 功能开发完成并合并到 Test `main`；
2. ChatGPT Review 通过；
3. 用户人工验收通过；

ChatGPT 才会把本文件改为 `Release Ready`。

## Release Ready 时必须记录

- Source Test commit
- Source branch（通常为 `main`）
- 本次发布内容
- 允许同步的文件 / 区域
- 不允许覆盖的 Prod 行为或文件
- 是否涉及数据结构、localStorage、IndexedDB、Gist、登录、导入导出
- Prod 发布分支名
- 发布后验证清单

## Prod 执行方式

Prod Workspace 独立打开 `personal-workstation-prod`。

本地 Git remote：

- `origin` → Prod
- `test` → Test

Prod 发布时通过 `git fetch test` 获取本文件记录的 Source Test commit。

禁止直接 `git merge test/main`；必须按发布清单做受控同步，并保留 Prod 正式环境行为。

## 发布完成后

- Prod push 发布分支
- ChatGPT Review
- Review 通过后合并 Prod `main`
- 用户人工验收
- ChatGPT 更新 Prod `docs/RELEASE_HISTORY.md`
- 本文件恢复为 `Idle`

## 当前发布候选

无。
