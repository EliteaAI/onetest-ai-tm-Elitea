---
id: ELITEA-4940
title: "Switching chats five times within 10 seconds during a run doesn't duplicate or lose steps"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Fast back-and-forth switching during a run keeps exactly one answer and the same step list as the server.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is H07.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Switch A → B → A five times within 10 s | Every switch lands |
| 3 | Stay in A until the end; note the steps and the answer | One answer `RUN-DONE H07` |
| 4 | Reload the page and note the steps again | The same 5 steps in the same order as before the reload and as `message_traces` |

**Note:** R7385LongRunner calls `waitSeconds` 3 times by design. Compare the step sequence, not unique names.

## Expected Final State

One answer, 5 steps, the same live and after a reload.

## Pass/Fail Criteria

**Pass:**
- Exactly one answer
- The live and reloaded step lists are identical and match `message_traces`

**Fail:**
- A duplicated or missing step, or a second answer

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`.
