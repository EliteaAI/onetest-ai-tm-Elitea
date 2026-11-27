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

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385Failer**, imported from [r7385-failer.agent.md](../../../../test-data/chat-runs-continue/r7385-failer.agent.md) (Agents → **Add agent** → **Import from file**) with step limit 3 (it needs 6 tool steps, so the run fails)
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385Failer as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Error text | "Maximum tool execution iterations (3) reached. Stopping tool execution." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Control: in A send `Go.`, stay to the end | Note the end state: the error text and 3 steps |
| 2 | Start a new conversation **A2** with R7385Failer, send `Go.` and open B | B opens |
| 3 | After the failure, look at A2's row | The "New response" dot |
| 4 | Open A2 | The same error text and 3 steps as the control (tool durations may differ); no streaming indicator |

## Expected Final State

The failure was reported on the row and in the chat.

## Pass/Fail Criteria

**Pass:**
- Dot after the failure
- The returned view equals the control

**Fail:**
- No dot, a spinner that never goes, or a different end state

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A, A2 and B, the agent R7385Failer and the toolkits `r7385_echo` and `r7385_jph`.
