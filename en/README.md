# research-foundation (English)

An English-only agent foundation plugin for research work: one permanent principles page plus ten philosophy-level process skills. The Chinese variant remains the default plugin in the repository root; installing this variant gives an English-only installation.

## Philosophy

As models become more capable, elaborate engineering workflows can become a burden. This plugin constrains agent behavior with lightweight principles and demanding completion criteria rather than step-by-step SOPs.

The process chain is **grounding (verify first) → brainstorming (diverge) → grilling (converge and obtain a decision) → executing-plans (implement faithfully)**. Discussion and execution remain separate; execution starts only after the plan is agreed.

## Permanent principles

[principles/foundation.md](principles/foundation.md) is injected by the `SessionStart` hook on startup, resume, clear, compaction, or fork. `SubagentStart` injects the main principles and the sub-agent increment.

## Skills

| Skill | Trigger | Purpose |
|---|---|---|
| `grounding` | Unclear context or advice is needed | Verify primary evidence before forming an opinion |
| `debugging` | Bug, error, failed test, regression, or anomaly | Find the root cause through a tight feedback loop |
| `brainstorming` | Before starting new research or analysis | Expand the option space before judging |
| `grilling` | A discussion requires an aligned decision | Ask one question at a time until the user decides |
| `executing-plans` | An agreed plan is ready | Implement exactly the agreed plan and verify it |
| `red-teaming` | Explicitly invoked by the user | Attack a named plan or claim with evidence |
| `handoff` | Explicitly invoked by the user | Compress a session for the next session |
| `writing-skills` | Writing or reviewing a skill | Maintain predictable, well-scoped skills |
| `delegating` | Assigning or supervising sub-agents | Delegate by context cost and verify returned artifacts |
| `truth-seeking` | Direction changes or a decision is requested | Keep changes in position driven by evidence |

## Installation

The repository marketplace provides two independent plugins. The default `research-foundation@dearcat` is Chinese. Install `research-foundation-en@dearcat` when you want the English-only variant.

### Claude Code

```bash
claude plugin marketplace add DearCaat/research-foundation-skills
claude plugin install research-foundation-en@dearcat
```

### Codex

```bash
codex plugin marketplace add DearCaat/research-foundation-skills --ref main
codex plugin add research-foundation-en@dearcat
```

After installation, reload plugins or start a new session. Codex may ask you to review and trust the command hook; after approval, `SessionStart` injects the English principles on startup, resume, clear, compaction, or fork.

### Grok Build

```bash
grok plugin marketplace add DearCaat/research-foundation-skills
grok plugin install research-foundation-en --trust
```

Grok loads the Claude-compatible plugin layout. Its allowed hook path triggers the hook but discards hook stdout, so the English principles are not re-injected into that turn’s context.

## Updating

Both variants are published from this repository. Bump the version in the corresponding plugin manifests when releasing an update, then refresh the marketplace and plugin in the target harness.
