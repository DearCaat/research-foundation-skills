# research-foundation

科研工作的 agent 基建插件：**一页常驻原则 + 十个哲学级过程 skill**。不做绑定具体业务的 skill，不搬工程 SOP。

## 语言版本与入口

同一仓库提供两个**互斥、可独立安装**的插件；不指定 `-en` 时默认使用中文：

| 版本 | 插件名 | 源目录 | README |
|---|---|---|---|
| 中文（默认） | `research-foundation` | 根目录 `./` | 本页 |
| 英文 | `research-foundation-en` | [`./en/`](en/) | [`en/README.md`](en/README.md) |

英文版的安装命令见下方各 harness 的“英文-only 版本”小节；只安装其中一个即可，不会把中英文内容打包到同一个已安装插件中。

## 哲学

随着模型能力增强，繁琐的工程化流程正在变成负担。约束 agent 过程的更好方式是：**原则性的轻量规范 + 苛刻的完成判据**，而不是逐步铺陈的 SOP。

本插件吸纳两个上游仓库的哲学（只取哲学，不搬其工程流程）：

- [mattpocock/skills](https://github.com/mattpocock/skills)：grilling（一次一问、决策归用户）、primary-source research、handoff、diagnosing-bugs 的 tight 反馈回路、prototype 的 throwaway 试算、writing-great-skills 的可预测性理论（invocation 二分、leading words、完成判据、negation 反噬、progressive disclosure）。
- [obra/superpowers](https://github.com/obra/superpowers)：using-superpowers 元规则（适用即必须调用）、循 skill 执行（follow exactly、checklist→todo、每次重读当前版本）、brainstorming 硬门槛、systematic-debugging 根因律、executing-plans 遇阻即停、dispatching-parallel-agents 并行纪律、verification-before-completion（无证据不声明完成、字面违反即精神违反）。

核心链路：**grounding（先查证）→ brainstorming（发散）→ grilling（收敛拍板）→ executing-plans（严格落地）**。讨论与执行分离；计划未共识不动手，执行中越界即停。

吸纳时的上游版本快照见 [UPSTREAM.md](UPSTREAM.md)，供日后对照上游更新做增量吸纳。

## 常驻原则

[principles/foundation.md](principles/foundation.md) 在支持 SessionStart stdout 注入的 harness 中由 hook 注入；Grok Build 则使用专用的 [global-rule 适配文件](grok/research-foundation.md)。八节：

1. **Skill 元规则**——任务开始前先查有无适用 skill，适用即调用
2. **循 skill 执行**——机械步骤与 gate 按文本走，判断类以成功条件的证据为准
3. **讨论 / 执行分离**——grounding → brainstorming → grilling → executing-plans；事实归证据，取舍归用户
4. **Sub-agent 调度**——context 是最稀缺的资源，探路过程外包、只回收结论；怎么派见 /delegating
5. **完成纪律**——无新鲜验证证据不声明完成
6. **输出精简**——只产出被要求或必需的文件
7. **写 skill 遵循 writing-skills**
8. **实事求是**——反驳落在证据上；改口须说清新证据或原推理错在哪，方向变化与决策时转 /truth-seeking 校准

## Skills

| skill | 触发 | 一句话 |
|---|---|---|
| `grounding` | 状态触发：需求不清、背景不明、要给建议时自动启动 | evidence before opinion，先查 primary sources 再开口 |
| `debugging` | 状态触发：bug、报错、测试失败、性能退化、意外实验结果或异常数据 | 先建 tight 反馈回路，以证据查明根因再修复 |
| `brainstorming` | 开新课题 / 新分析 / 新章节 / 新想法之前 | 先把选项面撑大，再评判 |
| `grilling` | 任何需要与用户对齐决策的讨论 | 一次一问，取舍逐个交用户拍板 |
| `executing-plans` | 有一份已共识的计划要落地 | 只做计划写明的事，遇阻即停、问而不猜 |
| `red-teaming` | 仅手动 `/red-teaming` | 拷打用户点名的方案/断言，交付被击破的前提或可抽查的未击破报告 |
| `handoff` | 仅手动 `/handoff` | 把会话压缩成交接文档给下一个 session |
| `writing-skills` | 写 skill、改 skill、review skill | skill 写作与维护规范（12 条原则 + review gates） |
| `delegating` | 准备委派、督办或核验 sub-agent 返回时 | 按 context 成本决定是否外包，并对产物与结论负责 |
| `truth-seeking` | 用户改变方向、要求决策，或 agent 准备随之改口时 | 区分证据、纠错、偏好与权责，阻止迎合性立场漂移 |

## 安装

本仓库同时是 Claude Code marketplace（`.claude-plugin/marketplace.json`）和 Codex marketplace（`.agents/plugins/marketplace.json`），市场名均为 `dearcat`。

### Claude Code

```bash
claude plugin marketplace add DearCaat/research-foundation-skills
claude plugin install research-foundation@dearcat
```

需要英文-only 版本时安装同一 marketplace 中的独立插件：

```bash
claude plugin install research-foundation-en@dearcat
```

（`owner/repo` 简写等价于完整 URL `https://github.com/DearCaat/research-foundation-skills.git`，SSH URL 亦可。）安装后 `/reload-plugins` 或开新会话生效；SessionStart hook 会在启动、恢复、清空、compact 或 fork 时注入 foundation。

### Codex

```bash
codex plugin marketplace add DearCaat/research-foundation-skills --ref main
codex plugin add research-foundation@dearcat
```

英文-only 版本：

```bash
codex plugin add research-foundation-en@dearcat
```

安装后开一个新的 Codex session。Codex 会在首次启用或 hook 更新后要求审查并信任该 command hook，信任后 SessionStart 会在启动、恢复、清空、compact 或 fork 时注入 foundation。

Codex 与 Claude Code 共用同一份 `hooks/hooks.json`：Codex 优先使用官方的 `${PLUGIN_ROOT}`，Claude Code 则回退到 `${CLAUDE_PLUGIN_ROOT}`。

### Grok Build

```bash
grok plugin marketplace add DearCaat/research-foundation-skills
grok plugin install research-foundation --trust

# 经 Grok Build 1.0.13 实测，本插件的 SessionStart / SubagentStart hook 未注册进运行时；
# 安装全局 rule，主会话和子 agent 都会自动加载它。
rules_dir="${GROK_HOME:-$HOME/.grok}/rules"
mkdir -p "$rules_dir"
curl -fsSL \
  https://raw.githubusercontent.com/DearCaat/research-foundation-skills/main/grok/research-foundation.md \
  -o "$rules_dir/research-foundation.md"

# 应列出 scope=global 的 research-foundation.md
grok inspect
```

不带 `-en` 的 `research-foundation` 是默认中文变体。Grok 会加载本插件的十个 skills，但经 Grok Build 1.0.13 实测不会把插件 hook 注册为可执行 hook；即使未来注册，`SessionStart` 的 stdout 也不会注入模型上下文。因此必须安装上面的 global rule。该 rule 包含“仅对子代理生效”的增量，实际 child session 会继承它。

英文-only 版本使用：

```bash
grok plugin install research-foundation-en --trust
rules_dir="${GROK_HOME:-$HOME/.grok}/rules"
mkdir -p "$rules_dir"
curl -fsSL \
  https://raw.githubusercontent.com/DearCaat/research-foundation-skills/main/en/grok/research-foundation.md \
  -o "$rules_dir/research-foundation.md"
```

### 更新

发布新版本：bump 两个 `plugin.json`（`.claude-plugin/` 与 `.codex-plugin/`）的 `version` 并推送到 `main`。已安装用户执行：

```bash
# Claude Code
claude plugin marketplace update dearcat
claude plugin update research-foundation@dearcat

# Codex
codex plugin marketplace upgrade dearcat
codex plugin add research-foundation@dearcat

# Grok Build（中文默认版）
grok plugin marketplace update DearCaat/research-foundation-skills
grok plugin update research-foundation
rules_dir="${GROK_HOME:-$HOME/.grok}/rules"
curl -fsSL \
  https://raw.githubusercontent.com/DearCaat/research-foundation-skills/main/grok/research-foundation.md \
  -o "$rules_dir/research-foundation.md"
```

Grok 英文版将上面两处 `research-foundation` 分别替换为 `research-foundation-en` 与 `en/grok/research-foundation.md`。更新后开一个新 session；`grok inspect` 应列出 scope=global 的 `research-foundation.md`。

然后开新 session（或 Claude Code 里 `/reload-plugins`）加载更新。

## 修改本插件

改任何 skill 前，先读并遵循 [skills/writing-skills/SKILL.md](skills/writing-skills/SKILL.md)——这也是本插件自身的红线。
