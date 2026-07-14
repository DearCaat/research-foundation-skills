# research-foundation

本仓库是一个 agent 插件：科研基建的哲学级过程 skill 与常驻原则。

任何在本插件生效环境下工作的 agent，必须先读取并遵循 [principles/foundation.md](principles/foundation.md)——它是 skill 元规则、讨论/执行分离、sub-agent 调度哲学、完成纪律与输出精简的单一权威位置。（Claude Code 通过 SessionStart hook 自动注入；其他 harness 由本文件引导。）

各 skill 位于 `skills/<name>/SKILL.md`，Codex 元数据在各自 `agents/openai.yaml`。修改或新建任何 skill 前，必须先读 `skills/writing-skills/SKILL.md`。
