# Skill writing and structure principles

This file is the single authority for writing and structure rules. `review_gates.md` contains only check questions.

## 1. Predictability

A skill makes a random system predictable, but mechanical and judgment work need different handles. For mechanical work, script extractable tasks (format checks, field scans, path checks, bulk replacement); do not make the model generate everything. For judgment work, make success conditions falsifiable rather than prescribing a path—forcing a capable model through a shape only reduces “doing it right” to “following the shape.”

## 2. Layer expression by testability

Hard-code what can be mechanically judged into scripts, schemas, and controlled values. Give judgment work a falsifiable target and specification; let the method vary. Keep numbered steps only when order is itself a constraint (confirm before acting, dry-run before write) or when premature action has been observed.

A specification is a discriminator, not a generator: it must be detailed enough for an independent reviewer to decide from the artifact, yet too coarse to copy mechanically. Do not disguise semantic quality or correctness as a mechanical gate.

Place unconditional decision rules in the permanent foundation. Put behavior triggered by external structure in a model-invoked skill; put triggers that would be corrupted by the behavior itself behind an existing signal or make them user-invoked. Put doctrine needed only while writing skills in these references.

## 3. Naming

Use a philosophy-level activity name in English kebab-case. The name itself should be a leading word, not a business object.

## 4. Invocation split

Use model invocation when an agent must trigger the skill autonomously, accepting the always-present description cost. Use `disable-model-invocation: true` when a user must trigger it, accepting the user’s memory cost. Keep the two harnesses paired: `disable-model-invocation` must match `policy.allow_implicit_invocation: false` in `openai.yaml`.

## 5. Descriptions

For model-invoked skills, put the trigger first, use one trigger phrase per scenario, and state exclusions. Do not enumerate natural-language variants.

## 6. Leading words

Anchor behavior to compact concepts that the model already knows (for example, grilling or tracer bullet). A weak word such as “carefully” does not anchor behavior.

## 7. Completion criteria

End every work unit with a checkable, exhaustive, falsifiable criterion. A valid result has a defect form: list deviations with evidence, or, when none are found, provide an auditable null report naming what was checked and against which invariant. “Confirmed correct” is not sufficient.

## 8. Negation backfire

Prefer positive target behavior. Use prohibitions only for hard red lines that cannot be stated positively, and pair each with the replacement action.

## 9. Layering and progressive disclosure

The entry point should contain responsibility, workflow, boundaries, required references, and output contract. Put stable, reusable, long material in one-purpose references or phase skills. Inline what every branch needs; move branch-specific detail down.

## 10. Script boundary

Scripts may check structure, format, paths, and explicit fields and emit risk or evidence. They must not issue semantic verdicts. Models and people judge meaning and correctness. Mechanical details that can be checked mechanically belong in scripts or schemas, not in judgment prose.

## 11. Compact base rules

- Front matter needs a unique kebab-case `name` and a `description` containing triggers and exclusions.
- Each rule states one executable, checkable action without no-op behavior.
- Use a single-tool structure for tools, a fixed-workflow controller for ordered phases, a route controller for routing, and an audit/update structure for bounded dry-run edits.

## 12. Necessary inputs and artifacts

Necessity, not count, is the criterion. Locate each required input before reading it and read only the needed portion. Every artifact, including an intermediate one, must have a stated purpose and consumer; specify its path when it must persist. Extra checks, schemas, gates, contracts, and abstractions need a named research conclusion they protect; if the reason is only “more engineering,” remove them. Before deleting a rule, ask which behavior would regress; if none can be named, it is redundant.
