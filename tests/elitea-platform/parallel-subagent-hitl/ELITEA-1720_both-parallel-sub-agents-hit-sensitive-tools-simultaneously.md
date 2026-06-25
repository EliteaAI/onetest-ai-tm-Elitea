---
id: ELITEA-1720
title: "Both parallel sub-agents hitting sensitive tools surface two approval cards simultaneously"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1720: Both Parallel Sub-Agents Hit Sensitive Tools — Both Cards Appear Simultaneously

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in **In-Process mode (Track 1)**, when two parallel sub-agents both hit sensitive tools, both approval cards appear simultaneously in the chat UI — regardless of which child hits HITL first.

**Behavior note:** In In-Process mode, HITL interrupts are aggregated at the parent level. If Sub-Agent A hits HITL first but Sub-Agent B is still executing, A waits for B. Once B also hits HITL, both cards surface together as a single aggregate interrupt. Execution resumes only after the user resolves ALL cards (approve/reject/block-with-comment).

**To enable Park+Dispatch mode (Track 2):** Set `parallel_subagent_dispatch: true` in indexer_worker config (Admin UI → Configuration → Advanced → pylon-indexer → indexer_worker → View → edit Raw Config → Save) and restart pylon-indexer.

## Preconditions

- Logged in to {{base_url}}
- **Execution mode: In-Process (Track 1)** — `parallel_subagent_dispatch` flag is absent or `false` in indexer_worker config
- Parent agent has two Application sub-agent tools
- Sub-Agent A has sensitive tool `create_issue`
- Sub-Agent B has sensitive tool `delete_file`
- Both configured to call their sensitive tools when invoked

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt dispatching both sub-agents in parallel | Both sub-agents dispatched simultaneously |
| 2 | Observe chat UI — even if one child reaches its sensitive tool before the other | No card appears yet while the sibling is still running |
| 3 | Wait until both sub-agents have reached their sensitive tools | Both approval cards appear together as a single aggregate interrupt |
| 4 | Inspect each card's content | Each card shows correct tool name and arguments; each belongs to correct sub-agent section |
| 5 | Verify no pre-execution | Neither tool has executed — both pending approval |
| 6 | Resolve ALL cards (approve/reject each) | Only after all cards are resolved does execution resume |

## Expected Final State

Two approval cards surfaced simultaneously as a single aggregate interrupt. Each shows correct tool name, arguments, and sub-agent attribution. Execution resumes only after all cards resolved.

## Pass/Fail Criteria

**Pass:**
- No card appears while a sibling is still running (waits for aggregate)
- Both cards appear together once both children hit HITL
- Each card shows correct tool name and arguments
- No tool executed before approval
- Execution resumes only after ALL cards resolved

**Fail:**
- One card appears before the sibling hits HITL (Park+Dispatch behavior in In-Process mode)
- Cards show wrong tool names or attribution
- A tool executes before approval
- Execution resumes after resolving only one card (remaining sibling's card ignored)
