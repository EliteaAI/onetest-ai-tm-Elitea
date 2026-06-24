---
id: ELITEA-1722
title: "Chat input is disabled while any HITL approval card is pending"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1722: Chat Input Disabled While HITL Approval Pending

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that the chat input field is locked while any HITL approval card is unresolved and re-enables after all cards are resolved and execution completes.

**Applies to:** Both execution modes.
- **In-Process (Track 1):** Input locked from the moment the aggregate interrupt surfaces until ALL cards resolved and execution completes. Default mode (`parallel_subagent_dispatch` absent or `false`).
- **Park+Dispatch (Track 2):** Input locked while any child's HITL card is pending. Each child resumes independently upon approval, but input remains locked until all pending cards are resolved. Enabled by setting `parallel_subagent_dispatch: true` in indexer_worker config and restarting pylon-indexer.

## Preconditions

- Logged in to {{base_url}}
- Agent with a sub-agent having a sensitive tool configured

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering a HITL approval card | Approval card appears |
| 2 | Attempt to type in chat input field while card is pending | Chat input is locked/disabled — cannot type or submit |
| 3 | Resolve the approval card (approve or reject) | Card resolved; execution continues |
| 4 | Wait for execution to complete | Parent produces final response |
| 5 | Attempt to type in chat input field | Input re-enabled; accepts new input |

## Expected Final State

Chat input disabled during pending HITL. Re-enables after all approvals resolved and execution complete.

## Pass/Fail Criteria

**Pass:**
- Chat input disabled while card pending
- Chat input re-enables after resolution

**Fail:**
- Chat input enabled during HITL pause
- Chat input stays locked after resolution
