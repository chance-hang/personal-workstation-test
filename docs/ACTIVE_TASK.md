# ACTIVE TASK

## 当前状态

Active

## 当前目标

继续原打卡历史功能，执行结构拆分后的阶段 B：

**断签备注 + 打卡记录图**

## 对应 Plan

主执行计划：

`docs/plans/2026-09-09-checkin-history-resume-after-split.md`

原始产品需求参考：

`docs/plans/2026-09-08-checkin-streak-history-and-mood-makeup.md`

## 当前阶段

阶段 B — 对应原 Task 3 + Task 4

## 当前分支

`codex/checkin-history-phase-b`

## 已完成基线

- Task 1：打卡历史统计核心逻辑，已合并
- Task 2：打卡概览与历史连续记录 UI，已合并
- 项目结构阶段 1：`index.html + styles.css + app.js`，已合并

不要重复实现以上内容。

## 执行要求

Codex 开始前：

1. 读取 `AGENTS.md`。
2. 读取本文件。
3. 读取 `docs/plans/2026-09-09-checkin-history-resume-after-split.md` 中“阶段 B”全部内容。
4. 仅在需要核对产品语义时读取原始 Plan 的 Task 3 / Task 4 相关部分。
5. 确认当前仓库为 `hb27bp49vk-source/personal-workstation-test`。
6. `git fetch`。
7. 同步最新 `main`。
8. 从最新 `main` 创建/切换到：`codex/checkin-history-phase-b`。
9. 如果工作区存在未提交修改，停止并汇报，不要自动清理或覆盖。

## 本轮只做

- 断签备注：新增 / 编辑 / 删除 / 刷新后保留
- 打卡记录图：复用现有日期/热力逻辑，展示打卡、断签、无数据、未来日期
- 日期详情：尽量让记录图与断签备注共用同一套详情入口
- 必要的数据兼容初始化
- 本阶段相关验证

当前文件职责：

- `index.html`：HTML 结构
- `styles.css`：样式
- `app.js`：业务逻辑

优先精准定位相关区域，不要为了理解项目而全量反复读取三个文件。

## 本轮禁止

- 不执行心情补卡（阶段 C）
- 不执行最终全局收尾（阶段 C）
- 不重新拆分 `app.js`
- 不引入 npm / 构建工具 / 框架
- 不修改无关模块
- 不全局格式化
- 不改变 localStorage 核心字段
- 不改变 GitHub Gist 加密同步协议
- 不重复实现 Task 1 / Task 2

## 完成后

完成并验证后：

1. 检查 `git diff`，确认只有阶段 B 相关修改。
2. commit 当前分支。
3. 提交信息：`feat: 增加断签备注与打卡记录图`
4. push `codex/checkin-history-phase-b` 到 GitHub。
5. 不合并 `main`。
6. 停止等待 ChatGPT Review。

## 汇报要求

用中文简要汇报：

- 阶段 B 是否完成
- 修改了哪些文件 / 主要函数
- 是否新增持久化字段，字段名是什么
- localStorage / 导出导入 / Gist 是否有协议变化
- 做了哪些验证
- 哪些验证受环境限制未完成
- commit SHA
- push 是否成功
- 当前分支
- 工作区是否干净
