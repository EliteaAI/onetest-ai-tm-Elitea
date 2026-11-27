---
id: ELITEA-4946
title: "The chat-list spinner disappears within 2 seconds when a run ends, is stopped or pauses"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** The row spinner follows the server: it goes within 2 s of the run ending, being stopped, or pausing for a question.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Agent **R7385AskUser**, imported from [r7385-askuser.agent.md](../../../../test-data/chat-runs-continue/r7385-askuser.agent.md) (Agents → **Add agent** → **Import from file**), internal tool Ask User on: waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2), answers `ASK-DONE post <id>`
- An idle conversation **B** (no run in it) to switch to
- Conversations **A** (R7385LongRunner) and **Q** (R7385AskUser)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Limit | 2 s from the server `is_streaming: false` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send `The word is M04.` in A, open B, and poll the conversation API every 0.5 s | When the run ends, A's spinner goes ≤ 2 s after the first poll with `is_streaming: false` |
| 2 | Send again in A and open B; while on B stop the run with `DELETE {{base_url}}/api/v2/elitea_core/task/prompt_lib/{project_id}/{run_uuid}` | The spinner goes ≤ 2 s after the server stop |
| 3 | Send `Look up a post for me.` in Q, open B, and wait until the run pauses | The spinner goes ≤ 2 s after the pause and the row shows the waiting dot |

**Note:** Take the run uuid from the latest `chat_run_status` "running" socket frame for that chat. An earlier one may belong to a finished run (DELETE → 404).

## Expected Final State

All three end states cleared the spinner in time.

## Pass/Fail Criteria

**Pass:**
- Each lag is ≤ 2 s (plus the 0.5 s poll step)

**Fail:**
- Any lag over 2 s, or the spinner never goes

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A, Q and B, the agents R7385LongRunner and R7385AskUser and the toolkits `r7385_echo` and `r7385_jph`.
