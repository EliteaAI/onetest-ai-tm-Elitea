---
id: ELITEA-4944
title: "An unsaved participant edit during a run shows only the editor dialog when switching chats"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** With unsaved participant edits, switching chats asks only about the edits, never about the running answer, and neither choice stops the run.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is M02.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message | The run starts |
| 2 | Open the participant's editor from the chat and change the instructions (don't save) | The edit is unsaved |
| 3 | Click B in the chat list | Only the dialog "You are editing agent now. Do you want to discard current changes and continue?" is shown |
| 4 | Click **Cancel** | The user stays in A and the run keeps streaming |
| 5 | Click B again and confirm | B opens; no `DELETE /task/...` |
| 6 | Wait for the end and open A | `RUN-DONE M02` |

## Expected Final State

The run completed; the unsaved edit was discarded on confirm.

## Pass/Fail Criteria

**Pass:**
- Only the editor dialog appears
- Cancel and Confirm both leave the run going

**Fail:**
- A streaming dialog appears, or either choice stops the run
