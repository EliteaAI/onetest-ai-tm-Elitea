---
id: ELITEA-4934
title: "Two chats run at once and Stop in one leaves the other running"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Runs in different chats are independent: both show the spinner, and Stop in one stops only that run.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversations **A** and **C**, both with R7385LongRunner as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `The word is SMK5A.` |
| Message in C | `The word is SMK5C.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the message in A, open C and send its message | Both rows show the running spinner |
| 2 | In C, wait for the first step and click **Stop** | Exactly one `DELETE /task/...` is sent, for C's run. The Stop button disappears, and C's row gets no dot |
| 3 | Open A | A's run is still going (Stop and "Agent is running…" shown) |
| 4 | Wait for A to end | A's answer is `RUN-DONE SMK5A` |

## Expected Final State

C was stopped; A finished normally.

## Pass/Fail Criteria

**Pass:**
- Both rows spin at once
- Stop in C affects only C

**Fail:**
- Stop in C stops A or sends a request for A's run
- Either row is missing the spinner while its run is going

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and C, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`.
