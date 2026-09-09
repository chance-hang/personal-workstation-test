# 个人工作台 Test → Prod 发布架构计划

## 状态

Active

## 背景

当前存在两个独立仓库：

- Test：`hb27bp49vk-source/personal-workstation-test`
- Prod：`hb27bp49vk-source/personal-workstation`

Test 已完成第一阶段结构拆分，当前为：

- `index.html`
- `styles.css`
- `app.js`

Prod 当前仍为单文件 `index.html`，且历史上存在正式环境专属行为，例如正式版刷新后的登录提示。

因此不能直接把 Test 的三个文件无脑覆盖到 Prod。需要先识别 Test / Prod 的真实差异，再把“环境差异”从“业务代码差异”里抽出来，最终建立可重复的 Test → Prod 发布流程。

## 总目标

建立以下长期规则：

1. 常规功能开发只在 Test 仓库进行。
2. Test 完成 ChatGPT Review 和人工验收后，才允许发布到 Prod。
3. Prod 不重新实现功能，只接收 Test 已验证版本。
4. 尽量让 Test / Prod 共享同一套业务代码。
5. 环境差异使用独立配置表达，避免 Test / Prod 长期分叉。
6. 发布过程必须可审查、可停止、可回滚。

## 目标结构

长期目标优先考虑：

```text
index.html
styles.css
app.js
env.js
```

其中：

- `index.html` / `styles.css` / `app.js`：尽量 Test / Prod 相同。
- `env.js`：只保存环境差异，不跨环境直接覆盖。

如果实际代码分析表明 `env.js` 不是最安全方式，可以调整命名或实现，但必须保持“共享业务代码 + 独立环境配置”的原则。

## 阶段 A — 差异审计与方案落地

### 目标

先在 Test 仓库中完成 Test / Prod 差异审计和发布方案设计，不修改 Prod 仓库业务代码。

### 必须检查

1. Test 当前 `index.html` / `styles.css` / `app.js` 与 Prod 单文件 `index.html` 的对应关系。
2. Prod 中是否存在 Test 没有的正式环境专属逻辑。
3. 重点检查：
   - 刷新后的 Chance 登录提示
   - 登录默认行为
   - localStorage 相关逻辑
   - Gist 加密同步
   - 数据导入 / 导出
   - 页面初始化顺序
   - 任何正式版专属文案或保护逻辑
4. 判断哪些差异属于：
   - 已过时的历史差异
   - 应继续保留的生产环境差异
   - 可以抽取到环境配置的差异
5. 给出最终迁移方案和明确文件边界。

### 本阶段允许

- 在 Test 仓库增加/更新文档。
- 如确认安全，可在 Test 分支中引入最小环境配置层并验证 Test 行为不变。
- 可以新增 `env.js`，但只能在方案明确且不破坏现有浏览器直接运行前提下进行。

### 本阶段禁止

- 不修改 `personal-workstation` 正式仓库。
- 不把 Test 文件复制到 Prod。
- 不发布任何正式版本。
- 不改变 localStorage 核心字段。
- 不改变 GitHub Gist 加密同步协议。
- 不重新拆分 `app.js`。
- 不引入 npm / 构建工具 / 框架。
- 不顺便重构无关业务代码。

### 验证

至少验证：

- Test 仍能浏览器直接运行。
- 现有主要页面、登录、数据保存和 Gist 同步路径不因环境配置改造而失效。
- 如果新增 `env.js`，Test 缺省环境和加载顺序清晰。
- 对 Prod 专属行为的保留方式有明确说明。

## 阶段 B — Prod 结构迁移

依赖：阶段 A Review 通过并人工确认。

目标：把 Prod 从单文件结构迁移到与 Test 一致的共享业务结构，同时保留正式环境专属行为。

阶段 B 开始前必须重新生成 ACTIVE_TASK，并明确 Prod 迁移步骤、备份点和回滚点。

## 阶段 C — 发布流程固化

依赖：阶段 B 验证通过。

目标：建立稳定的 Test → Prod 发布清单，包括：

- Source Test commit
- Target Prod repo
- 可同步文件
- 禁止覆盖文件
- 环境配置保留项
- 发布前检查
- 发布后验证
- 回滚方式

最终由 `docs/RELEASE.md` 记录当前待发布状态。

## 完成标准

当以下条件全部满足时，本计划完成：

1. Test / Prod 业务结构基本一致。
2. 环境差异被明确隔离。
3. Test 是唯一常规开发入口。
4. Prod 不再直接重新实现功能。
5. 有清晰的 Release 文档和执行步骤。
6. 至少完成一次 Test → Prod 的受控发布验证。
