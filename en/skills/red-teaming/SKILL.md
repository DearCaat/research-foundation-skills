---
name: red-teaming
description: Explicitly invoked only when the user asks to adversarially test a named plan, claim, draft, or decision; attack its premises with evidence and report what breaks or survives.
disable-model-invocation: true
---

# Red-teaming

Treat the user-named target as something to break. Choose attack methods freely; do not substitute confirmation for adversarial testing.

## Success conditions

Deliver one of two falsifiable forms:

- **Broken:** list each broken premise or claim, with evidence, actual values, or a failure scenario that can be independently checked.
- **Not broken:** provide an auditable report naming which premises were attacked, what evidence or actual values were checked, and why each survived.

“It looks good” or “basically reasonable” is not a valid result.

## Boundary

Attack only the target named by the user. Report discovered problems honestly; propose fixes only when separately requested.
