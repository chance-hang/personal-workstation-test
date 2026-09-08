# AGENTS.md

## 项目说明

这是“个人工作台”的测试版。

当前应用采用单文件架构：
- 主程序：`index.html`
- HTML、CSS、JavaScript 均内联在 `index.html`
- 无构建步骤
- 无 npm / Node.js 依赖
- 浏览器直接运行
- 数据主要存储于 localStorage
- 支持 GitHub Gist 加密同步

除非任务明确要求，不要主动把单文件架构拆分为多个文件。

## Codex 工作原则

### 1. 先理解任务，再读取代码

不要为了“全面理解项目”而默认读取整个 `index.html`。

优先：
- 根据任务定位相关模块
- 搜索函数名、DOM id、`data-module`、注释标题
- 只读取相关区域及必要上下文

避免重复读取完整 `index.html`。

### 2. 严格控制修改范围

每个任务只修改与任务直接相关的代码。

禁止：
- 顺便重构其他模块
- 全局格式化 `index.html`
- 大规模改名
- 改变无关 CSS
- 修改无关业务逻辑

如果发现额外问题，记录并汇报，不要自行扩大任务范围。

### 3. 保持现有架构

除非任务计划明确要求：
- 不引入 React / Vue / Angular
- 不引入 npm 构建系统
- 不拆分 `index.html`
- 不增加后端
- 不更换存储方案

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

Codex 应优先执行计划中的明确 Task，而不是自行重新设计整个方案。

例如：

`Implement Task 2 from docs/plans/2026-09-08-example.md`

只执行指定 Task。

## 完成任务时

Codex 必须汇报：
- 修改了哪些区域
- 修改了哪些函数
- 是否改变数据结构
- 是否涉及 localStorage
- 是否涉及 GitHub Gist 同步
- 如何验证
- 是否发现但未处理的其他问题

不要在没有说明的情况下修改数据兼容性。
