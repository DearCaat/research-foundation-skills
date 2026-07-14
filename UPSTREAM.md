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
