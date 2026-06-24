---
id: ELITEA-1721
title: "Approving one parallel HITL card and rejecting the other routes each to the correct child"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1721: Approve One Child, Reject the Other — Each Routes Independently

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in **In-Process mode (Track 1)**, when two parallel sub-agents are both paused for HITL (aggregate interrupt), approving one and rejecting the other routes each decision to the correct derived thread_id independently.

**Behavior note:** In In-Process mode, both cards appear together as an aggregate interrupt. The user must resolve ALL cards before execution resumes. Each decision (approve/reject) routes to the correct child thread. Only after all cards are decided does the parent proceed with the combined outcomes.

## Preconditions

- Logged in to {{base_url}}
- **Execution mode: In-Process (Track 1)** — `parallel_subagent_dispatch` flag absent or `false`
- Same setup as ELITEA-1720: both parallel sub-agents paused with two approval cards visible (aggregate interrupt state)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | From the aggregate interrupt state (both cards visible), click Approve on Sub-Agent A's card | Card is marked as decided; Sub-Agent A's tool has NOT executed yet (waits for all cards to be resolved) |
| 2 | Click Reject on Sub-Agent B's card | Card is marked as decided; all cards now resolved |
| 3 | Observe execution resume | Sub-Agent A's sensitive tool executes exactly once; Sub-Agent B's tool does NOT execute |
| 4 | Observe parent synthesis response | Parent correctly attributes Sub-Agent A's success and Sub-Agent B's rejection |
| 5 | Verify no cross-contamination | Results are correctly attributed to each sub-agent |

## Expected Final State

Sub-Agent A tool ran once. Sub-Agent B tool did not run. Parent synthesizes both outcomes correctly. Execution only resumed after both cards were resolved.

## Pass/Fail Criteria

**Pass:**
- Execution does not resume until ALL cards are resolved
- Sub-Agent A tool executed exactly once after all decisions made
- Sub-Agent B tool not executed
- Parent synthesis reflects correct outcome for each

**Fail:**
- Execution resumes after resolving only one card
- Sub-Agent B tool executes despite rejection
- Sub-Agent A tool doesn't execute despite approval
- Cross-contamination of results
