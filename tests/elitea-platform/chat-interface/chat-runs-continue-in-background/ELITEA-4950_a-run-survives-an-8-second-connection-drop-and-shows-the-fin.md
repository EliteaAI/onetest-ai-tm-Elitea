---
id: ELITEA-4950
title: "A run survives an 8-second connection drop and shows the final answer without a reload"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** After the socket reconnects, the chat catches up with the run's end without a page reload.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversation **A** with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is M08.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Set the browser offline for 8 s (DevTools → Network → Offline), then online | The connection comes back |
| 3 | Stay in A to the end, without a reload | `RUN-DONE M08` with 5 steps = `message_traces` |

## Expected Final State

The run completed and the chat caught up after the reconnect.

## Pass/Fail Criteria

**Pass:**
- The final answer and 5 steps show without a reload

**Fail:**
- The run is stopped, or the chat stays stuck until a reload
