# research-foundation (English)

This directory is the English variant of the agent plugin: philosophy-level research process skills and permanent principles.

Every agent working with this plugin must first read and follow [principles/foundation.md](principles/foundation.md). It is the single authority for skill meta-rules, discussion/execution separation, sub-agent scheduling, completion discipline, and concise output. (Claude Code injects it through the SessionStart hook; other harnesses are guided by this file.)

Skills live under `skills/<name>/SKILL.md`, with Codex metadata in each `agents/openai.yaml`. Before modifying or creating a skill, read `skills/writing-skills/SKILL.md`.
