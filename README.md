# research-foundation

科研工作的 agent 基建插件：**一页常驻原则 + 六个哲学级过程 skill**。不做绑定具体业务的 skill，不搬工程 SOP。

## 哲学

随着模型能力增强，繁琐的工程化流程正在变成负担。约束 agent 过程的更好方式是：**原则性的轻量规范 + 苛刻的完成判据**，而不是逐步铺陈的 SOP。

本插件吸纳两个上游仓库的哲学（只取哲学，不搬其工程流程）：

- [mattpocock/skills](https://github.com/mattpocock/skills)：grilling（一次一问、决策归用户）、primary-source research、handoff、writing-great-skills 的可预测性理论（invocation 二分、leading words、完成判据、negation 反噬、progressive disclosure）。
- [obra/superpowers](https://github.com/obra/superpowers)：using-superpowers 元规则（适用即必须调用）、循 skill 执行（follow exactly、checklist→todo、每次重读当前版本）、brainstorming 硬门槛、executing-plans 遇阻即停、verification-before-completion（无证据不声明完成、字面违反即精神违反）。

核心链路：**grounding（先查证）→ brainstorming（发散）→ grilling（收敛拍板）→ executing-plans（严格落地）**。讨论与执行分离；计划未共识不动手，执行中越界即停。

吸纳时的上游版本快照见 [UPSTREAM.md](UPSTREAM.md)，供日后对照上游更新做增量吸纳。

## 常驻原则

[principles/foundation.md](principles/foundation.md) 由 SessionStart hook 每次会话注入（含 /clear 与 compact 后），七节：

1. **Skill 元规则**——任务开始前先查有无适用 skill，适用即调用
2. **循 skill 执行**——按序不跳步不遗漏，判据满足才进下一步
3. **讨论 / 执行分离**——grounding → brainstorming → grilling → executing-plans
4. **Sub-agent 调度哲学**——按任务性质选成本档；用户给定 prompt 逐字执行
5. **完成纪律**——无新鲜验证证据不声明完成
6. **输出精简**——只产出被要求或必需的文件
7. **写 skill 遵循 writing-skills**

## Skills

| skill | 触发 | 一句话 |
|---|---|---|
| `grounding` | 状态触发：需求不清、背景不明、要给建议时自动启动 | evidence before opinion，先查 primary sources 再开口 |
| `brainstorming` | 开新课题 / 新分析 / 新章节 / 新想法之前 | 先把选项面撑大，再评判 |
| `grilling` | 任何需要与用户对齐决策的讨论 | 一次一问，决策逐个交用户拍板 |
| `executing-plans` | 有一份已共识的计划要落地 | 只做计划写明的事，遇阻即停、问而不猜 |
| `handoff` | 仅手动 `/handoff` | 把会话压缩成交接文档给下一个 session |
| `writing-skills` | 写 skill、改 skill、review skill | skill 写作与维护规范（12 条原则 + review gates） |

## 安装

### Claude Code

```bash
claude plugin marketplace add /mnt/d/twh/research-foundation
claude plugin install research-foundation@twh
```

（或仓库在其他路径 / 远程 git 时，将第一行参数换成对应路径或 `owner/repo`。）

更新：修改本仓库并 bump `.claude-plugin/plugin.json` 的 `version` 后——

```bash
claude plugin marketplace update twh
claude plugin update research-foundation@twh
```

然后 `/reload-plugins` 或开新会话生效。

### Codex

```bash
codex plugin marketplace add /mnt/d/twh/research-foundation
codex plugin add research-foundation@twh
```

清单在 `.codex-plugin/plugin.json`（`skills` 为单路径字符串，指向 `./skills/`，Codex 递归发现 `SKILL.md`）；本地 marketplace 定义在 `.agents/plugins/marketplace.json`。常驻原则复用同一份 `hooks/hooks.json`——Codex 的 hooks 与 Claude Code 同 schema，且兼容 `CLAUDE_PLUGIN_ROOT` 变量；首次会话 Codex 会要求信任该 hook（unmanaged hook 审查机制），确认后 SessionStart 即注入 foundation。每个 skill 的 Codex 元数据在各自 `agents/openai.yaml`。

更新：bump `.codex-plugin/plugin.json` 的 `version` 后重新 `codex plugin add research-foundation@twh` 刷新快照。

## 修改本插件

改任何 skill 前，先读并遵循 [skills/writing-skills/SKILL.md](skills/writing-skills/SKILL.md)——这也是本插件自身的红线。
