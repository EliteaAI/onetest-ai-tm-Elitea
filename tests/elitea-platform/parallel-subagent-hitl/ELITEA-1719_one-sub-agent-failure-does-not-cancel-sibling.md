---
id: ELITEA-1719
title: "One sub-agent failure does not cancel sibling sub-agent execution"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1719: One Sub-Agent Failure Does Not Cancel Sibling

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when one sub-agent fails during parallel fan-out, the sibling continues to completion and the parent handles both outcomes gracefully.

**Applies to:** Both execution modes (In-Process Track 1 and Park+Dispatch Track 2). Failure isolation is fundamental to both modes.

## Preconditions

- Logged in to {{base_url}}
- Parent agent has two Application sub-agent tools
- Sub-Agent A is intentionally broken (invalid config/endpoint)
- Sub-Agent B is correctly configured

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt dispatching both Sub-Agent A and Sub-Agent B in parallel | Both sub-agents are dispatched |
| 2 | Observe Sub-Agent B's execution | Sub-Agent B completes successfully; result visible in UI |
| 3 | Observe Sub-Agent A's outcome | Sub-Agent A's failure surfaced as an error ToolMessage (not crash) |
| 4 | Observe parent agent behavior | Parent continues using Sub-Agent B's result; generates synthesis response |
| 5 | Verify session state | Session remains active — no crash, no hang |

## Expected Final State

Parent receives Sub-Agent B's result and Sub-Agent A's error ToolMessage. Session completes normally.

## Pass/Fail Criteria

**Pass:**
- Sub-Agent B result present in parent response
- Sub-Agent A failure surfaced as ToolMessage
- Session continues and completes

**Fail:**
- Sub-Agent B cancelled when A fails
- Session hangs or crashes
- Parent receives no results
