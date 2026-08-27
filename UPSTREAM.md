# 上游吸纳记录

记录每次吸纳时上游仓库的版本快照，供日后 diff 增量更新（对照该 commit 与上游最新 main 的差异，只看被吸纳文件）。

## 2026-07-14（v0.1.0–v0.1.1 初次吸纳）

| 上游 | commit（main） | 上游版本 | 被吸纳文件 |
|---|---|---|---|
| [mattpocock/skills](https://github.com/mattpocock/skills) | `66898f60e8c744e269f8ce06c2b2b99ce7660d5f`（2026-07-13） | plugin 1.2.0 | `skills/productivity/grilling`、`skills/productivity/handoff`、`skills/productivity/writing-great-skills`（含 GLOSSARY.md）、`skills/engineering/research`、`skills/engineering/implement`、`skills/engineering/to-spec`（Out of Scope 思想）、`.agents/invocation.md` |
| [obra/superpowers](https://github.com/obra/superpowers) | `d884ae04edebef577e82ff7c4e143debd0bbec99`（2026-07-02） | plugin 6.1.1（本机安装副本同版） | `skills/using-superpowers`、`skills/brainstorming`、`skills/executing-plans`、`skills/verification-before-completion`；`hooks/hooks.json` 与 `.codex-plugin/plugin.json` 作 schema 参照 |

## 2026-07-14（v0.2.0 第二次定向吸纳）

| 上游 | commit（main） | 上游版本 | 本次新增被吸纳文件 |
|---|---|---|---|
| [mattpocock/skills](https://github.com/mattpocock/skills) | `66898f60e8c744e269f8ce06c2b2b99ce7660d5f`（2026-07-13） | plugin 1.2.0 | `skills/engineering/diagnosing-bugs`、`skills/productivity/prototype` |
| [obra/superpowers](https://github.com/obra/superpowers) | `d884ae04edebef577e82ff7c4e143debd0bbec99`（2026-07-02） | plugin 6.1.1（本机安装副本同版） | `skills/systematic-debugging`、`skills/dispatching-parallel-agents` |

## 2026-07-14（v0.2.1 第三次定向吸纳）

| 上游 | commit（main） | 上游版本 | 本次新增被吸纳文件 |
|---|---|---|---|
| [mattpocock/skills](https://github.com/mattpocock/skills) | `66898f60e8c744e269f8ce06c2b2b99ce7660d5f`（2026-07-13） | plugin 1.2.0 | `skills/engineering/wayfinder`（context pointer 回挂结论、按 token 预算定尺寸） |
| [obra/superpowers](https://github.com/obra/superpowers) | `d884ae04edebef577e82ff7c4e143debd0bbec99`（2026-07-02） | plugin 6.1.1（本机安装副本同版） | `skills/subagent-driven-development`（sub-agent 隔离 context、保全主上下文） |

落点：writing-skills `references/principles.md` 第 12 条「输入与产物的必要性」。

吸纳原则：只取哲学，不搬工程 SOP；对应落点见 [README](README.md) 与 `principles/foundation.md`。

## 2026-08-26（v0.4.0 增量吸纳）

| 上游 | commit / tag | 上游版本 | 本次新增被吸纳内容 |
|---|---|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | tag `v6.3.0`（2026-08-12） | plugin 6.3.0 | `skills/brainstorming`（ceremony scales with the task；单向棘轮）、`skills/subagent-driven-development`（Model Selection 的显式指定模型与 turn-count 判据；task-reviewer-prompt 的 Do Not Trust the Report 与 Missing/Extra/Misunderstood 三分）、`skills/receiving-code-review`（YAGNI Check：不需要的功能不要加）、PR1934（detritus 三形态；其 eval-gated 删除机制未吸纳，本地无 behavior eval 基建） |
| [mattpocock/skills](https://github.com/mattpocock/skills) | main（2026-08-24） | plugin 1.2.3 | 本轮复核后未新增吸纳；round/frontier 批量提问经社区实测反弹（#771/#840/#895/#274/#44）明确不吸纳 |

落点：`principles/foundation.md` §2（rule/gate 分层）、§3（小事不走全套）、§4（sub-agent 调度重写）、§6（先答科研问题再谈工程完备）；writing-skills `references/principles.md` 第 2 条（机械化前置）、第 12 条（机制受必要性约束；删规则文本的判据）。

不吸纳：上游 brainstorming 的 spike / bounded / architectural 三档分类——其锚点是"仓库里有无现成流程可读"，科研语境无等价客观锚点，分档会退化为 agent 自评并招致升档判据膨胀，改为只保留"产物随任务缩放、批准不缩放"一条判据；prompt 模板、字段表、状态取值、报告格式（插件只写哲学）；"sub-agent 不得再派 sub-agent"类条款；Rulings-not-stalls 与必停清单（用户裁定保留原红线）；TDD iron law、worktree、review package、ledger、circuit breaker 等软件工程 SOP。

## 2026-08-27（v0.5.0 委派哲学收敛）

本轮没有扩大上游吸纳范围，继续收敛 v0.4.0 已吸纳的 sub-agent 哲学。落点：`principles/foundation.md` §4 改为以主 agent context 成本决定是否委派，§3 增停止判据，§6 增范围边界，末尾新增 §8「实事求是」以避免既有章号顺延；新增 `delegating` skill 与 `principles/foundation-subagent.md`。foundation 常驻页由 1926 缩至 1702 字符。

原 `writing-skills/references/principles.md` 第 12 条「大范围探索交 sub-agent 隔离承担……」已并入 foundation §4，原处只保留输入先定位、按需读取。

`SubagentStart` hook 初测在既有 VS Code 长驻 app-server 中未触发；根因是 app-server 启动早于 plugin hook 更新且不热重载，并非 hook 协议无效。新起 Codex runtime 的真实 child transcript 已出现 `hooks.additional_context` 注入的 foundation 与子代理增量；更新 hook 后须重载 Codex 宿主再验证。
