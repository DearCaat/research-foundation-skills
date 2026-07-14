---
name: writing-skills
description: 写 skill、改 skill、review skill、拆分或合并 skill、把稳定流程沉淀为 skill 时使用；只处理 skill 本身的入口、结构、规则分层与 review，不用于执行 skill 所描述的业务任务本身。
---

# Writing Skills

用于创建和维护 skill 本身：入口、结构、规则分层与 review。不执行 skill 所描述的业务任务。

## 何时用 / 不用

用于：

- 创建顶层 skill、子 skill 或工具型 skill。
- 维护已有 SKILL.md、references/、scripts/ 的职责边界与规则表达。
- 拆分、合并、重组 skill 的规则层级。
- 检查 skill 的冗余、冲突、职责漂移或触发不清。
- 把临时流程沉淀为正式 skill 结构。

不用于：

- 执行相邻业务 skill 描述的任务本身。
- 对业务内容做事实核验或改写。
- 一次性的 tmp/、会话记录、audit 输出整理。

## 必读引用

- [references/principles.md](references/principles.md)：写作与结构原则。
- [references/review_gates.md](references/review_gates.md)：修改后检查。

## 维护 workflow

1. 定范围：只处理用户点名的 skill、文件及其强依赖；目标不清先问，不顺手重构相邻 skill。
2. 读现状：先读目标 SKILL.md，再按需读其 references/、子 skill、脚本；确认不接管相邻业务入口。
3. 最小补丁：按 principles.md 设计改动范围与文本分层。
4. 落地：controller 只留路由、顺序、边界、红线；细则下沉 references/ 或阶段子 skill。
5. 过 review gates。

## 创建 workflow

1. 写清职责边界：解决什么 / 不解决什么 / 何时触发 / 何时不触发；与现有 skill 重叠时优先扩展已有入口。
2. 选结构：按 principles.md 结构模式速查选型，结构服务职责。
3. 写入口：每个可调用 skill 必须有 SKILL.md，front matter 含唯一 kebab-case name 与含触发+排除场景的 description。
4. 分层：SKILL.md 只放职责、流程、边界、必读引用、输出约定；稳定长内容下沉 references/。
5. 过 review gates。

## 红线

- 默认最小改动。
- 删除、移动、批量改写、外部写入前必须经用户确认。
- review gates 适用项必须通过；N/A 须说明理由；无法满足的适用项标 blocked 并说明缺什么。

## 输出约定

汇报：改了哪些文件、为何是最小必要改动、gates 结果、风险与待决问题。
