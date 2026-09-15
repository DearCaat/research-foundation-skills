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

## 2026-08-27（v0.5.1 求真校准）

新增 model-invoked `truth-seeking`：在用户改变方向、要求决策或 agent 准备随之改口时，区分新证据、推理纠错、用户偏好与权责决定；证据不足转 `grounding` 补证。foundation §8 只增加触发路由，具体判据留在 skill，避免重复常驻原则。

## 2026-09-16（v0.6.0 强模型校准）

本轮不吸纳上游新文件，依据厂商一手来源校准常驻页三处文本，使其停止过度约束强模型：

| 来源 | 类型 | 被采用的判断 |
|---|---|---|
| [OpenAI: Rethinking skills and prompts for GPT-6 Astra](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra)（2026-09-11） | 博客，无量化评测 | 过度具体的指导现在会阻碍；"要求停下等 review 会把模型拉向更早的停止点，检查那是不是你真的需要做的决定"；不同模型对同一指令的约束强度不同 |
| [Anthropic: Prompting Claude Fable 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5) | 官方文档 | "为旧模型写的 skill 常常过于 prescriptive，会降低产出质量"；停顿只限不可逆动作、真正的范围变更、只有用户能给的输入；暴露 context 预算会诱发提前收尾 |
| [Anthropic: Prompting Claude Fable 5.1](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1) | 官方文档 | "对可逆且源于原请求的动作直接做，只为破坏性动作或真正的范围变更停" |
| [Anthropic: Prompting Claude Opus 5](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5) | 官方文档 | 指令会被字面执行；过度委派警告 |
| [Anthropic: Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices) | 官方文档 | 自由度按任务脆弱性定；Haiku 问"够不够"、Opus 问"是否过度解释"；先建评测 |
| [obra/superpowers](https://github.com/obra/superpowers) v6.3.0 | 上游 | 对照：using-superpowers 原文有 "If it turns out wrong for the situation, you don't have to use it"，v0.1.0 吸纳时丢失，本轮补回 |

落点（四份镜像同步：`principles/foundation.md`、`grok/research-foundation.md`、`en/principles/foundation.md`、`en/grok/research-foundation.md`）：
- §1：删「1% 也调用、绝不自我合理化」，改为「适用即调用，拿不准也调用；读完发现不适用可退出并说明」——正向陈述并补退出口，与 writing-skills principles 第 8 条一致。
- §2：删「字面违反即精神违反……成本高于遵守本身」——该论证只对机械 gate 成立，而 §2 已把机械 gate 送进 hook，留在 rule 上即「加重语气」，与 §2 末句自相矛盾。
- §3：删「批准不缩放，一句话方案也要停下等同意」（推翻 v0.4.0 保留裁定，依据是上述新证据），改为「停不停不看任务大小，按下段可逆性裁决」，消除与同节「可逆且低成本自决」的冲突。`skills/brainstorming` Gate 同步改引 §3。
- §4：委派首要动机由「context 最稀缺」改为「独立与并行；需要独立判断或干净背景的审查另开 worker」，保留「只回收结论与指针」与「一条命令距离自己做」。

不改（用户裁定）：SubagentStart 继续注入整页 foundation——哲学也要给执行者看，越弱越需要。异议留痕：§3 停顿规则进执行型 sub-agent 会让它返回而非继续；§3 改后此成本已下降。弱模型需要的确定性放派发 prompt（delegating「给执行器求确定」）与 harness 适配文件，不分两套哲学。

未做：behavior eval。本轮全部是文本层比对，未实测；厂商来源亦为"内部测试"级，Astra 博文无数字。
