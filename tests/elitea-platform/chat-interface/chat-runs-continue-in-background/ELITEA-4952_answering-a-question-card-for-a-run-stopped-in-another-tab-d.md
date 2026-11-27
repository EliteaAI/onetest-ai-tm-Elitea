---
id: ELITEA-4952
title: "Answering a question card for a run stopped in another tab doesn't start a new run"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** If a paused run is stopped in another tab, its question card in the first tab can't restart it.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385AskUser**, imported from [r7385-askuser.agent.md](../../../../test-data/chat-runs-continue/r7385-askuser.agent.md) (Agents → **Add agent** → **Import from file**), internal tool Ask User on: waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2), answers `ASK-DONE post <id>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385AskUser as the participant
- Two browser tabs
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `Look up a post for me.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In tab 1, send the message in A and open B; wait until A's row shows the waiting dot | The run is paused on the question |
| 2 | In tab 2, open A and stop the run with `DELETE {{base_url}}/api/v2/elitea_core/task/prompt_lib/{project_id}/{run_uuid}` (a paused Ask User run has Skip, not Stop) | 204; the run status goes from waiting to stopped |
| 3 | In tab 1, open A and try to answer the card (Post 2 → Continue) | Either the card is already gone, or answering starts nothing: no new message group, no `is_streaming: true`, no `ASK-DONE` |
| 4 | Wait for the next sync | A matches a reload, with no run indicator |

**Note:** A stopped paused run removes the whole exchange (no answer text branch of Stop).

## Expected Final State

The stopped run stayed stopped.

## Pass/Fail Criteria

**Pass:**
- No new run starts from tab 1

**Fail:**
- Answering in tab 1 restarts the run or creates a new answer

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B, the agent R7385AskUser and the toolkits `r7385_echo` and `r7385_jph`.
