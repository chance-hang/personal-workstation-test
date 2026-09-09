# AGENTS.md

## 项目说明

这是“个人工作台”的测试版。

当前应用基线仍以浏览器直接运行、无构建步骤、无 npm / Node.js 依赖为原则。
数据主要存储于 localStorage，并支持 GitHub Gist 加密同步。

历史上项目采用单文件架构：
- 主程序：`index.html`
- HTML、CSS、JavaScript 均内联在 `index.html`

除非当前 `docs/ACTIVE_TASK.md` 或对应 Plan 明确授权，不要主动改变项目结构、拆分文件或引入框架/构建系统。
如果当前任务明确是架构整理或文件拆分任务，则以该任务文件和 Plan 的范围为准。

## Codex 工作原则

### 1. 先理解任务，再读取代码

开始前优先读取：
1. `AGENTS.md`
2. `docs/ACTIVE_TASK.md`（如果存在）
3. ACTIVE_TASK 指向的 Plan

不要为了“全面理解项目”而默认读取整个大文件。

优先：
- 根据任务定位相关模块
- 搜索函数名、DOM id、`data-module`、注释标题
- 只读取相关区域及必要上下文

避免重复读取完整大文件。

### 2. 严格控制修改范围

每个任务只修改与任务直接相关的代码。

禁止：
- 顺便重构其他模块
- 全局格式化
- 大规模改名
- 改变无关 CSS
- 修改无关业务逻辑

如果发现额外问题，记录并汇报，不要自行扩大任务范围。

### 3. 保持现有技术路线

除非当前任务计划明确要求：
- 不引入 React / Vue / Angular
- 不引入 npm 构建系统
- 不增加后端
- 不更换存储方案
- 不改变 GitHub Gist 加密同步协议

文件拆分只有在 ACTIVE_TASK / Plan 明确授权时才能进行。

## 多电脑协作规则

GitHub 是唯一共享状态。

任何一台电脑开始 Codex 任务之前：
1. 检查当前分支
2. `git fetch`
3. 同步最新 `main`
4. 为当前任务使用独立分支

分支示例：
- `codex/fix-habit-checkin`
- `codex/add-budget-filter`
- `codex/fix-mobile-nav`

不同电脑不得同时修改同一个任务分支。

不要让多台电脑同时直接修改 `main`。

## 任务计划

复杂任务必须先有计划。

计划文件位于：

`docs/plans/`

当前要执行什么，以：

`docs/ACTIVE_TASK.md`

为入口。

Codex 应优先执行 ACTIVE_TASK 指向的明确阶段，而不是自行重新设计整个方案。

## 完成任务时

Codex 必须汇报：
- 修改了哪些区域
- 修改了哪些函数/文件
- 是否改变数据结构
- 是否涉及 localStorage
- 是否涉及 GitHub Gist 同步
- 如何验证
- 是否发现但未处理的其他问题

如果 ACTIVE_TASK 明确要求完成后 commit/push，则按其要求执行；否则不要擅自合并 `main`。

不要在没有说明的情况下修改数据兼容性。
