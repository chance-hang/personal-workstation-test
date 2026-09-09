# ACTIVE TASK

## 当前状态

Active

## 当前目标

执行“个人工作台 Test → Prod 发布架构”阶段 B：

**Prod 单文件结构机械拆分**

## 对应 Plan

`docs/plans/2026-09-09-test-prod-release-architecture.md`

## 当前工作区

本机 Codex Workspace：`personal-workstation`

其中：

- Test：`personal-workstation-test`
- Prod：`personal-workstation-prod`

## 当前任务分支

在 Prod 仓库创建：

`codex/prod-split-single-file`

## 本轮目标

把 Prod 当前单文件 `index.html` 机械拆分成：

- `index.html`
- `styles.css`
- `app.js`

核心原则：

**只改变文件组织，不改变正式版业务行为。**

本阶段不是 Test → Prod 功能发布，不把 Test 当前业务代码覆盖到 Prod。

## 开始前

1. 读取：
   - `personal-workstation-test/AGENTS.md`
   - `personal-workstation-test/docs/ACTIVE_TASK.md`
   - `personal-workstation-test/docs/plans/2026-09-09-test-prod-release-architecture.md`
   - `personal-workstation-test/docs/test-prod-diff-audit.md`
2. 检查 Test 与 Prod 两个仓库的 Git 状态。
3. 两边都执行 `git fetch`。
4. 确认 Test `main` 已同步最新 GitHub。
5. 确认 Prod 当前 `main` 已同步最新 GitHub。
6. 如果任一仓库存在未提交修改，停止并汇报，不自动清理。
7. 记录 Prod 当前 `main` HEAD SHA，作为本次回滚基线。
8. 在 Prod 最新 `main` 上创建/切换分支：`codex/prod-split-single-file`。

## 本轮只允许修改

Prod 仓库：`personal-workstation-prod`

允许：

- 修改 `index.html`
- 新增 `styles.css`
- 新增 `app.js`

Test 仓库本轮只读，不修改任何 Test 业务代码或文档。

## 迁移方式

### B1. CSS 机械拆分

将 Prod `index.html` 中现有主 `<style>` 内容原样迁移到 `styles.css`。

要求：

- 尽量保持原顺序和原内容
- 不重写选择器
- 不格式化整个 CSS
- 不顺便清理重复样式
- `index.html` 改为正确引用 `styles.css`

### B2. JavaScript 机械拆分

将 Prod `index.html` 中现有主业务脚本原样迁移到 `app.js`。

要求：

- 保持脚本执行顺序
- 保持 DOM 初始化时机
- 保持正式登录行为
- 保持 localStorage 无前缀命名空间
- 保持现有 IndexedDB 镜像行为
- 保持 Gist 登录 / 同步逻辑
- 保持导入 / 导出逻辑
- 不把 Test 的 `app.js` 覆盖到 Prod
- 不引入 ES Module
- 不引入构建系统

### B3. HTML 收口

`index.html` 最终只保留页面结构与外链资源引用。

确保：

- `styles.css` 正确加载
- `app.js` 正确加载
- 原有资源路径不变
- 原有 DOM id / class / data 属性不变
- 不新增 `env.js`

## 必须保留的 Prod 行为

本次迁移必须保持：

- Prod 无前缀 localStorage
- 正式 Gist 同步可用
- 正式账户登录逻辑
- 刷新后的登录提示 / 默认登录行为
- 现有 IndexedDB 镜像与恢复路径
- 导入 / 导出
- 页面初始化顺序
- 正式环境现有文案和保护逻辑

## 关于敏感凭据

用户已明确这是个人项目，并接受现有源码凭据风险。

因此本轮：

- 不轮换凭据
- 不迁移凭据
- 不删除凭据
- 不把凭据复制到 Test
- 不在汇报或文档中输出凭据内容
- 凭据问题不阻塞本次结构迁移

## 本轮禁止

- 不修改 Test 业务代码
- 不把 Test 的 `index.html` / `styles.css` / `app.js` 覆盖 Prod
- 不同步打卡历史等新功能到 Prod
- 不新增 `env.js`
- 不升级 IndexedDB 实现
- 不改变 localStorage key
- 不改变 Gist 协议
- 不改变登录流程
- 不改变导入 / 导出格式
- 不重构函数
- 不重新拆分 `app.js`
- 不引入 npm / Node / 框架
- 不全局格式化
- 不合并 Prod `main`

## 验证

至少完成以下验证：

1. 检查拆分前后 HTML / CSS / JS 内容对应关系，确认业务脚本没有遗漏或重复。
2. 浏览器直接打开 Prod `index.html`，确认页面可正常加载。
3. 检查控制台没有因拆分导致的新语法错误 / 资源加载错误。
4. 主要 Tab / 页面切换正常。
5. 刷新后的正式登录提示 / 默认登录行为与拆分前一致。
6. localStorage 正式数据仍能读取，不出现 `wbtest_` 前缀。
7. IndexedDB 初始化与镜像路径没有被改动。
8. 导入 / 导出入口正常。
9. Gist 登录 / 同步相关代码路径未被改动；如果不适合使用真实数据验证，可做静态路径核对并明确说明未实测项。
10. 检查 `git diff`，应主要表现为从 `index.html` 移出 CSS / JS 到两个新文件，而不是大规模业务重写。

## 完成后

在 Prod 分支：

1. 检查 `git diff`。
2. commit。
3. 推荐提交信息：`refactor: 拆分正式版单文件结构`
4. push `codex/prod-split-single-file` 到 GitHub。
5. 不合并 `main`。
6. 停止等待 ChatGPT Review。

## 汇报要求

用中文简短汇报：

- Prod 回滚基线 SHA
- 是否完成三文件拆分
- 修改了哪些 Prod 文件
- 是否修改任何业务逻辑
- 正式登录 / localStorage / IndexedDB / Gist / 导入导出是否保持
- 做了哪些验证
- 哪些项目未实际验证及原因
- commit SHA
- push 是否成功
- 当前分支
