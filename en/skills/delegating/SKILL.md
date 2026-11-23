---
name: delegating
description: When assigning, supervising, reusing, restarting, or verifying a sub-agent, choose delegation by context cost, brief it precisely, watch artifacts, and verify what returns.
---

# Delegating

Place outsourced work with the right worker while keeping its process and conclusions falsifiable.

Whether to delegate follows §4 of the standing principles; dispatch mutually independent sub-tasks in parallel within one response.

## Reuse or restart

- Before dispatching, inventory existing workers, their problem domains, and local context. Reuse a worker when the domain and assumptions still hold; restart when the task changes domain, premises changed, old context would mislead, or an independent review is needed.

## Brief shape

- A new worker that does not inherit your context needs a self-contained first prompt with the necessary context and no dangling pronouns. A reused worker, or one that inherits your context, needs only the increment. For a review that must be independent, use a worker that does not inherit your context, and give it the material, not your conclusion.
- Give an executor a concrete outcome and narrow freedom; give a reviewer or judgment-heavy worker the goal, evidence, and boundary without prescribing a mechanical path.
- State that its user is the main agent, and tell it to ask rather than guess when only you can answer.
- When creating a worker, set the model and effort explicitly when the host supports it rather than relying on defaults; when the host requires inheritance, check the inherited configuration against the requirements. On return, verify the configuration that actually ran and mark anything you cannot verify as unverified. When a configuration the user named cannot be met, report the gap and switch only with the user’s consent. When reusing a worker, keep its configuration unless it conflicts with the new task.
- If the user supplied a sub-agent prompt, execute it verbatim.

## Delegation is not hand-off

An active status does not prove useful work or correctness. Judge progress by artifacts, counts, logs, and processes. Before dispatching, define what “done” looks like; take over if that artifact is not produced.

## Verify returns

Treat every returned claim as unverified. Check numbers and facts against primary artifacts, challenge the reasons given, and resolve conflicts between results before adopting them.

## Completion criterion

Every dispatch or reuse points to a problem domain and context rationale; every adopted conclusion points to primary evidence or an artifact personally checked by the main agent.
