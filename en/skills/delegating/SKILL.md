---
name: delegating
description: Use when choosing an executor for an independent sub-task, dispatching or reusing a worker, supervising one that is running, or verifying what handed-off work returns. Running existing commands yourself under an agreed plan, and work you do yourself from start to finish, follow executing-plans.
---

# Delegating

Place outsourced work with the right executor while keeping its process and conclusions falsifiable.

Whether to delegate follows §4 of the standing principles; dispatch mutually independent sub-tasks in parallel within one response.

## Choose the executor

- First state what the task needs—determinism, batch scale, reviewable reasons, or gathering material and acting as it goes—and choose a script, decision model, direct LLM API call, or harness accordingly.
- When comparing ways to execute, or checking the failure signs specific to the executor in use, read the matching section of [references/executors.md](references/executors.md).
- Honor the model or configuration the user named for every model call: when it cannot be met, report the gap and switch only with the user’s consent; set aside results that the response confirms ran under a different configuration.
- For calls that cost money, trial runs included, stay within the authorization the user gave; ask before going beyond it.
- The “Reuse or restart” and “Brief shape” sections below apply only to workers that hold a session.

## Reuse or restart

- Before dispatching, inventory existing workers, their problem domains, and local context. Reuse a worker when the domain and assumptions still hold; restart when the task changes domain, premises changed, old context would mislead, or an independent review is needed.

## Brief shape

- A new worker that does not inherit your context needs a self-contained first prompt with the necessary context and no dangling pronouns. A reused worker, or one that inherits your context, needs only the increment. For a review that must be independent, use a worker that does not inherit your context, and give it the material, not your conclusion.
- Give an executor a concrete outcome and narrow freedom; give a reviewer or judgment-heavy worker the goal, evidence, and boundary without prescribing a mechanical path.
- State that its user is the main agent, and tell it to ask rather than guess when only you can answer.
- When creating a worker, set the model and effort explicitly when the host supports it rather than relying on defaults; when the host requires inheritance, check the inherited configuration against the requirements. On return, verify the configuration that actually ran and mark anything you cannot verify as unverified. When reusing a worker, keep its configuration unless it conflicts with the new task.
- If the user supplied a sub-agent prompt, execute it verbatim.

## Delegation is not hand-off

An active status does not prove useful work or correctness. Judge progress by artifacts, counts, logs, and processes. Before dispatching, define what “done” looks like; take over if that artifact is not produced.

## Verify returns

Treat every returned claim as unverified. Check numbers and facts against primary artifacts, challenge the reasons given, and resolve conflicts between results before adopting them.

## Completion criterion

The choice of executor points to the task need it serves; every dispatch or reuse points to a problem domain and context rationale; every adopted conclusion points to primary evidence or an artifact personally checked by the main agent.
