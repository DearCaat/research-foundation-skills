# Skill review gates

The rules live in `principles.md`; this file contains only the questions to check. Every applicable gate must pass. Mark N/A with a reason; mark blocked with the missing requirement. “Mostly compliant” or “fix later” is not a pass.

## Scope

- Did the change stay within the user-named skills, files, and hard dependencies?
- Did it avoid incidental refactoring of neighboring skills?

## Minimal change

- Is every reordering or rewrite necessary?
- Were existing files preferred over parallel new files where that would suffice?

## Language

- Is the prose in the intended language, precise, and concise?
- Is every rule executable and checkable?
- Is there any no-op behavior that the model would do by default?

## Redundancy

- Does each rule appear in one place only?
- Does the controller avoid copying phase detail from child skills?

## Conflicts

- Does the description avoid triggering neighboring skills?
- Are read/write and user-confirmation rules consistent with the existing workflow?
- Are any existing rules contradictory?

## Naming

- Is `name` unique and kebab-case?
- Is it an activity rather than a business object?
- Do title, directory, name, and description identify the same responsibility?

## Invocation and criteria

- Is the invocation choice justified?
- Are the two harnesses paired?
- Is each work-unit criterion falsifiable rather than a confirmation phrase?
- Is judgment specification precise enough to settle disputes but too coarse to copy mechanically?
- Can prohibitions be stated as positive target behavior?

## Script boundary

- Do scripts stay within structural, format, path, and field checks?
- Do semantic verdicts remain with a model or person?
- Are mechanically decidable details implemented in scripts or schemas?

## Necessary inputs and artifacts

- Is every read task-relevant and limited to the needed fragment?
- Does every artifact have a purpose and consumer?
- Were no unrequested output files added?
- Were required verification and evidence reads retained?
