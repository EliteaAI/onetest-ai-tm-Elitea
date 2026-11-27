---
id: ELITEA-4948
title: "A run that fails while the user is away gets the New response dot and shows the error on return"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A failed run is marked on the row like a finished one, and on return the chat shows the same end state as when the user stayed.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385Failer** ([instructions](../../../../test-data/chat-runs-continue/r7385-failer.instructions.md)) with step limit 3 (it needs 6 tool steps, so the run fails)
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385Failer as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Error text | "Maximum tool execution iterations (3) reached. Stopping tool execution." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Control: in A send `Go.`, stay to the end | Note the end state: the error text and 3 steps |
| 2 | Clear A, send again and open B | B opens |
| 3 | After the failure, look at A's row | The "New response" dot |
| 4 | Open A | The same error text and 3 steps as the control (tool durations may differ); no streaming indicator |

## Expected Final State

The failure was reported on the row and in the chat.

## Pass/Fail Criteria

**Pass:**
- Dot after the failure
- The returned view equals the control

**Fail:**
- No dot, a spinner that never goes, or a different end state
