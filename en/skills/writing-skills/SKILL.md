---
name: writing-skills
description: When creating, modifying, reviewing, splitting, or merging a skill, maintain its entry point, structure, rule layering, and review discipline. Do not use it to execute the business task described by a neighboring skill.
---

# Writing skills

Maintain skill entry points, structure, boundaries, and review quality; do not execute the business task described by the skill.

## Use / do not use

Use this skill to create or maintain top-level skills, child skills, and tool skills; maintain `SKILL.md`, references, and scripts; split, merge, or reorganize skills; check redundancy, conflicts, scope drift, and triggers; and turn a temporary process into a formal skill.

Do not use it for fact-checking or rewriting business content, executing an adjacent business skill, or organizing one-off temporary or session artifacts.

## Required reading

- [references/principles.md](references/principles.md): writing and structure principles.
- [references/review_gates.md](references/review_gates.md): post-edit checks.

## Maintenance workflow

1. Define scope: handle only the skills, files, and hard dependencies named by the user; ask when the target is unclear; do not refactor neighboring skills.
2. Read the current state: read the target `SKILL.md`, then only the references, child skills, and scripts it needs; confirm that you are not taking over a neighboring business entry point.
3. Make the smallest patch: use `principles.md` to design the edit range and text layers.
4. Implement: keep the controller to routing, order, boundaries, and red lines; move stable detail into references or phase skills.
5. Pass the review gates.

## Creation workflow

1. State the responsibility boundary: what it solves, what it does not, when it triggers, and when it does not. When it overlaps an existing skill, extend the existing entry point first.
2. Choose a structure that serves the responsibility.
3. Write the entry point: every callable skill needs `SKILL.md` with a unique kebab-case `name` and a `description` containing triggers and exclusions.
4. Layer the content: `SKILL.md` holds responsibility, workflow, boundaries, required references, and output contract; stable, long content goes into references.
5. Pass the review gates.

## Red lines

Default to minimal edits. Deleting, moving, bulk-rewriting, or writing externally requires user confirmation. Every applicable review gate must pass; mark N/A with its reason and blocked with the missing requirement.

## Output contract

Report changed files, why the patch is minimal, gate results, risks, and unresolved decisions.
