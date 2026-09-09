# ACTIVE TASK

## 当前状态

Active

## 当前目标

继续原打卡历史功能，执行结构拆分后的阶段 C：

**心情补卡 + 打卡历史集成回归**

## 对应 Plan

主执行计划：

`docs/plans/2026-09-09-checkin-history-resume-after-split.md`

原始产品需求参考：

`docs/plans/2026-09-08-checkin-streak-history-and-mood-makeup.md`

## 当前阶段

阶段 C — 对应原 Task 5 + Task 6

## 当前分支

`codex/checkin-history-phase-c`

## 已完成基线

- Task 1：打卡历史统计核心逻辑，已合并
- Task 2：打卡概览与历史连续记录 UI，已合并
- 阶段 B：断签备注 + 打卡记录图，已合并
- 阶段 B Review 修正：断签日期超过 3 天时折叠展示，已合并
- 项目结构已拆分为：`index.html + styles.css + app.js`

不要重复实现以上内容。

## 执行要求

Codex 开始前：

1. 读取 `AGENTS.md`。
2. 读取本文件。
3. 读取 `docs/plans/2026-09-09-checkin-history-resume-after-split.md` 中“阶段 C”全部内容。
4. 仅在需要核对产品语义时读取原始 Plan 的 Task 5 / Task 6 相关部分。
5. 确认当前仓库为 `hb27bp49vk-source/personal-workstation-test`。
6. `git fetch`。
7. 同步最新 `main`。
8. 从最新 `main` 创建/切换到：`codex/checkin-history-phase-c`。
9. 如果工作区存在未提交修改，停止并汇报，不要自动清理或覆盖。

## 本轮只做

### C1. 心情补卡

- 允许选择过去日期补录心情。
- 当天没有心情记录时新增。
- 当天已有心情记录时进入编辑，不创建重复记录。
- 禁止未来日期。
- 今天继续保留现有正常心情入口，不破坏现有使用方式。
- 复用现有 `S.moods`、`MOODS`、样式和保存逻辑，不建立第二套心情数据源。
- 保存后立即刷新心情相关 UI、年度热力图和打卡记录相关显示。

### C2. 集成回归

重点检查 Task 1～5 组合后的完整行为：

- 打卡概览、连续记录、断签备注、打卡记录图、心情补卡状态一致。
- 不产生重复事件绑定。
- 历史数据没有新增字段时仍能正常打开。
- `checkinBreakNotes` 与现有数据一起正常保存、导出、导入、同步。
- `S.moods` 继续沿用原有日期键结构。
- localStorage 核心字段不改名、不迁移。
- GitHub Gist 加密协议不改变。
- 手机尺寸没有明显破版。
- 只修复本功能引入的问题，不做无关重构。

当前文件职责：

- `index.html`：HTML 结构
- `styles.css`：样式
- `app.js`：业务逻辑

优先精准定位心情、日期详情、热力图、打卡记录、持久化与同步相关区域，不要全量反复读取三个文件。

## 本轮禁止

- 不重新设计打卡历史功能。
- 不重新实现 Task 1 / Task 2 / 阶段 B。
- 不重新拆分 `app.js`。
- 不引入 npm / 构建工具 / 框架。
- 不修改无关模块。
- 不全局格式化。
- 不改变 localStorage 核心字段。
- 不改变 GitHub Gist 加密同步协议。
- 不做与本功能无关的 UI 重设计。

## 验证

至少验证：

1. 过去无心情记录日期可以补录。
2. 过去已有心情记录日期可以修改，且不会重复。
3. 未来日期不能补录。
4. 保存后页面立即反映新的心情。
5. 刷新页面后心情记录仍存在。
6. 年度热力图 / 打卡记录相关显示能正确刷新。
7. 断签备注新增、编辑、删除仍正常。
8. 打卡记录图日期点击仍正常。
9. 连续记录折叠/展开仍正常。
10. 老数据缺少 `checkinBreakNotes` 时正常。
11. 导出 / 导入 / Gist 序列化路径没有被意外改坏。
12. 桌面端和移动端没有明显破版。

## 完成后

1. 检查 `git diff`，确认只有阶段 C 相关修改。
2. commit 当前分支。
3. 提交信息：`feat: 完成心情补卡与打卡历史集成`
4. push `codex/checkin-history-phase-c` 到 GitHub。
5. 不合并 `main`。
6. 停止等待 ChatGPT Review。

## 汇报要求

用中文简要汇报：

- 阶段 C 是否完成
- 修改了哪些文件 / 主要函数
- 心情补卡入口放在哪里
- 是否改变数据结构
- localStorage / 导出导入 / Gist 是否有协议变化
- 做了哪些验证
- 哪些验证受环境限制未完成
- commit SHA
- push 是否成功
- 当前分支
- 工作区是否干净
