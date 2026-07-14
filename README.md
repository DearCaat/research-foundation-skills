# research-foundation

科研工作的 agent 基建插件：**一页常驻原则 + 七个哲学级过程 skill**。不做绑定具体业务的 skill，不搬工程 SOP。

## 哲学

随着模型能力增强，繁琐的工程化流程正在变成负担。约束 agent 过程的更好方式是：**原则性的轻量规范 + 苛刻的完成判据**，而不是逐步铺陈的 SOP。

本插件吸纳两个上游仓库的哲学（只取哲学，不搬其工程流程）：

- [mattpocock/skills](https://github.com/mattpocock/skills)：grilling（一次一问、决策归用户）、primary-source research、handoff、diagnosing-bugs 的 tight 反馈回路、prototype 的 throwaway 试算、writing-great-skills 的可预测性理论（invocation 二分、leading words、完成判据、negation 反噬、progressive disclosure）。
- [obra/superpowers](https://github.com/obra/superpowers)：using-superpowers 元规则（适用即必须调用）、循 skill 执行（follow exactly、checklist→todo、每次重读当前版本）、brainstorming 硬门槛、systematic-debugging 根因律、executing-plans 遇阻即停、dispatching-parallel-agents 并行纪律、verification-before-completion（无证据不声明完成、字面违反即精神违反）。

核心链路：**grounding（先查证）→ brainstorming（发散）→ grilling（收敛拍板）→ executing-plans（严格落地）**。讨论与执行分离；计划未共识不动手，执行中越界即停。

吸纳时的上游版本快照见 [UPSTREAM.md](UPSTREAM.md)，供日后对照上游更新做增量吸纳。

## 常驻原则

[principles/foundation.md](principles/foundation.md) 由 SessionStart hook 每次会话注入（含 /clear 与 compact 后），七节：

1. **Skill 元规则**——任务开始前先查有无适用 skill，适用即调用
2. **循 skill 执行**——按序不跳步不遗漏，判据满足才进下一步
3. **讨论 / 执行分离**——grounding → brainstorming → grilling → executing-plans；事实归证据，决策归用户
4. **Sub-agent 调度哲学**——按任务性质选成本档；用户给定 prompt 逐字执行
5. **完成纪律**——无新鲜验证证据不声明完成
6. **输出精简**——只产出被要求或必需的文件
7. **写 skill 遵循 writing-skills**

## Skills

| skill | 触发 | 一句话 |
|---|---|---|
| `grounding` | 状态触发：需求不清、背景不明、要给建议时自动启动 | evidence before opinion，先查 primary sources 再开口 |
| `debugging` | 状态触发：bug、报错、测试失败、性能退化、意外实验结果或异常数据 | 先建 tight 反馈回路，以证据查明根因再修复 |
| `brainstorming` | 开新课题 / 新分析 / 新章节 / 新想法之前 | 先把选项面撑大，再评判 |
| `grilling` | 任何需要与用户对齐决策的讨论 | 一次一问，决策逐个交用户拍板 |
| `executing-plans` | 有一份已共识的计划要落地 | 只做计划写明的事，遇阻即停、问而不猜 |
| `handoff` | 仅手动 `/handoff` | 把会话压缩成交接文档给下一个 session |
| `writing-skills` | 写 skill、改 skill、review skill | skill 写作与维护规范（12 条原则 + review gates） |

## 安装

本仓库同时是 Claude Code marketplace（`.claude-plugin/marketplace.json`）和 Codex marketplace（`.agents/plugins/marketplace.json`），市场名均为 `dearcat`。

### Claude Code

```bash
claude plugin marketplace add DearCaat/research-foundation-skills
claude plugin install research-foundation@dearcat
```

（`owner/repo` 简写等价于完整 URL `https://github.com/DearCaat/research-foundation-skills.git`，SSH URL 亦可。）安装后 `/reload-plugins` 或开新会话生效；SessionStart hook 会注入 `principles/foundation.md`（含 `/clear` 与 compact 后重注入）。

### Codex

```bash
codex plugin marketplace add DearCaat/research-foundation-skills --ref main
codex plugin add research-foundation@dearcat
```

安装后开一个新的 Codex session。Codex 会在首次启用或 hook 更新后要求审查并信任该 command hook，信任后 SessionStart 即注入 foundation。

两端共用同一份 `hooks/hooks.json`，以 `${CLAUDE_PLUGIN_ROOT}` 定位插件目录——这是 Claude Code 唯一支持的插件根变量，Codex 官方为兼容 Claude 插件 hook 同样提供它。

### 更新

发布新版本：bump 两个 `plugin.json`（`.claude-plugin/` 与 `.codex-plugin/`）的 `version` 并推送到 `main`。已安装用户执行：

```bash
# Claude Code
claude plugin marketplace update dearcat
claude plugin update research-foundation@dearcat

# Codex
codex plugin marketplace upgrade dearcat
codex plugin add research-foundation@dearcat
```

然后开新 session（或 Claude Code 里 `/reload-plugins`）加载更新。

## 修改本插件

改任何 skill 前，先读并遵循 [skills/writing-skills/SKILL.md](skills/writing-skills/SKILL.md)——这也是本插件自身的红线。
