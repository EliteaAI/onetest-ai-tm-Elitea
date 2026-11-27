---
id: ELITEA-4941
title: "After a page reload during a run, the chat row spins and the chat opens in progress"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A reload (F5) on another chat doesn't lose the run state: the row still spins and the chat opens in progress.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is H08.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Open B and reload the page (F5) | B reloads |
| 3 | Look at A's row | The row shows the running spinner. `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` has `has_running_task: true` for A |
| 4 | Open A while it is running | The run is in progress: Stop, "Agent is running…" and the finished steps |
| 5 | Wait for the end | `RUN-DONE H08` with 5 steps = `message_traces` |

## Expected Final State

The run survived the reload and finished.

## Pass/Fail Criteria

**Pass:**
- The spinner is back after the reload
- A opens in progress and ends with 5 steps

**Fail:**
- After the reload the row looks idle while the run is going, or A opens without the run

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`.
