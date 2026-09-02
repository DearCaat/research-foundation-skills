---
name: handoff
description: Explicitly invoked when the user asks to hand the current session to a later session; compress goals, decisions, progress, artifacts, and next steps into a self-contained handoff document.
disable-model-invocation: true
---

# Handoff

Compress the current session so the next agent can continue without replaying the conversation.

## Method

- Record the goal, settled conclusions, current progress, and next action.
- Link existing artifacts—plans, notes, commits, and files—rather than copying their contents.
- Remove secrets and personal information.
- Include a “Suggested skills” section naming the skills the next session should use first.
- Store the document in the system temporary directory, not in the project.

## Trimming

If the user specifies the next session’s purpose, keep only material relevant to that purpose. Record where the current conversation history, including sub-agent history, is stored.
