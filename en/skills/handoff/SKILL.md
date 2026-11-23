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
- Store the document where the receiving session can read it (for a cross-machine handoff, a location both sides can read), not in the project; on delivery, give an absolute path the receiver can use directly.

## Trimming

If the user specifies the next session’s purpose, keep only material relevant to that purpose. Record where the current conversation history, including sub-agent history, is stored.
