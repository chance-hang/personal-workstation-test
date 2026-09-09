# 单文件架构拆分：index.html → index.html + styles.css + app.js

## 状态

Active

## 背景

当前“个人工作台”长期采用单文件 `index.html`，HTML、CSS、JavaScript 全部内联。随着功能增多，单文件体积较大，AI 编程工具在定位、读取和修改时需要重复扫描同一大文件，增加执行时间、上下文开销和 Review 成本。

本 Plan 的目标不是业务重构，而是先进行一次低风险、可验证的物理文件拆分，为后续 AI 协作和继续开发打卡功能降低上下文开销。

原打卡功能 Plan：
`docs/plans/2026-09-08-checkin-streak-history-and-mood-makeup.md`

在本 Plan 完成并合并前，原 Plan 的 Task 3–6 暂停执行。

## 总目标

把当前：

```text
index.html
  ├─ HTML
  ├─ CSS
  └─ JavaScript
```

拆成：

```text
index.html
styles.css
app.js
```

要求：**只改变文件组织，不改变产品行为。**

## 明确不做

本轮禁止：

- 不引入 React / Vue / Angular。
- 不引入 npm、Vite、Webpack 或任何构建工具。
- 不新增后端。
- 不把 `app.js` 继续拆成多个业务模块。
- 不重构业务逻辑。
- 不重命名现有函数、DOM id、数据字段。
- 不全局格式化代码。
- 不顺便修复无关问题。
- 不改变页面视觉设计。
- 不改变 localStorage 数据结构。
- 不改变导入/导出格式。
- 不改变 GitHub Gist 加密同步协议。

如果拆分过程中发现必须修改业务逻辑才能工作，先停止并汇报，不要自行扩大范围。

## 阶段 1 — 机械拆分

建议分支：

`codex/split-single-file-phase-1`

### 目标

将原 `index.html` 中的主要内联 CSS 和主要内联 JavaScript 原样迁移到外部文件，并由 `index.html` 正确引用。

### 要求

1. 从最新 `main` 创建独立分支。
2. 将现有主样式块迁移到根目录 `styles.css`。
3. 将现有主 JavaScript 迁移到根目录 `app.js`。
4. 在 `index.html` 中使用普通浏览器可直接加载的方式引用：
   - `<link rel="stylesheet" href="styles.css">`
   - `<script src="app.js"></script>`
5. 保持脚本执行时机与原实现一致。若原脚本依赖 DOM 已创建，外链脚本的位置必须保持等价语义，不能为了“规范”擅自改为 module/defer，除非验证证明完全等价且确有必要。
6. 保持所有函数、全局变量、事件绑定、HTML 结构和 CSS 选择器语义不变。
7. 原有第三方外链脚本/样式不要无故调整顺序。
8. 不修改任何现有数据模型和持久化协议。

### 对内联代码的处理原则

本轮目标是“主要 CSS + 主要 JS”拆分，不追求 100% 清除所有内联属性或小型内联事件。

例如以下内容不要求重构：

- HTML 元素上的 `style="..."`
- `onclick="..."` 等现有内联事件属性
- 为业务模板字符串服务的小段样式字符串

不要为了彻底消灭内联代码扩大修改范围。

## 验证要求

Codex 必须尽可能验证拆分前后行为等价，至少检查：

1. `index.html` 能在浏览器直接打开，不需要本地服务器或构建步骤。
2. 页面无明显控制台语法错误。
3. 主导航和各模块可以正常切换。
4. 习惯打卡功能可正常渲染。
5. Task 1/2 已完成的打卡历史统计和 UI 仍可正常渲染。
6. localStorage 原数据仍能正常加载。
7. 修改数据后刷新页面仍能保留。
8. 与 GitHub Gist 同步相关代码仍存在且未改变协议。
9. 页面样式没有因 CSS 引用顺序变化而明显失真。
10. 检查 `git diff`，确认修改核心是“搬移代码 + 增加引用”，没有夹带业务重构。

若环境无法完整做浏览器交互测试，必须明确说明哪些已验证、哪些需要用户视觉确认。

## 完成条件

阶段 1 完成时，仓库根目录应至少包含：

```text
index.html
styles.css
app.js
```

并且应用仍保持：

- 浏览器直接运行
- 无 npm / Node.js 依赖
- 无构建步骤
- 原 localStorage 兼容
- 原 GitHub Gist 同步兼容
- UI 与功能无计划内变化

## Git 与 Review 流程

阶段 1 完成后：

1. Codex 自行检查 diff。
2. commit 到任务分支。
3. push 任务分支到 GitHub。
4. 不合并 `main`。
5. 停止，等待 ChatGPT Review。

建议提交信息：

`refactor: 拆分单文件为 HTML CSS JS`

## 后续阶段

阶段 1 Review 并稳定合并后，暂时不要立即继续把 `app.js` 拆成多个模块。

先恢复原打卡 Plan 的 Task 3，观察：

- Codex 执行速度是否改善
- token / 上下文消耗是否下降
- Review 是否更容易

只有验证确实有收益且 `app.js` 仍明显过大时，再另建第二阶段 Plan 讨论按业务域拆分 JavaScript。
