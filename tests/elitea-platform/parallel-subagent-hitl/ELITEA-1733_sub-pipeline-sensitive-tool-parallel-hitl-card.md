---
id: ELITEA-1733
title: "Sub-pipeline with sensitive tool in parallel fan-out surfaces HITL approval card correctly"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1733: Sub-Pipeline With Sensitive Tool in Parallel Fan-Out — HITL Card Appears

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a sub-pipeline containing a sensitive tool is invoked in a parallel fan-out, the HITL approval card appears correctly and the approval/rejection routes the decision to the correct child.

**Applies to:** Both execution modes.
- **In-Process (Track 1):** If the sibling sub-agent/pipeline is still running, the HITL card waits for all children to settle before surfacing as an aggregate interrupt. Default mode (`parallel_subagent_dispatch` absent or `false`).
- **Park+Dispatch (Track 2):** HITL card appears immediately when the sub-pipeline hits the sensitive tool. Enabled by setting `parallel_subagent_dispatch: true` in indexer_worker config and restarting pylon-indexer.

## Preconditions

- Logged in to {{base_url}}
- Parent agent has two Application tools: one sub-agent (safe, no sensitive tools) and one sub-pipeline (contains a sensitive tool)
- Both triggered in one parallel turn

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt dispatching both the safe sub-agent and the sub-pipeline with sensitive tool | Both dispatched in parallel |
| 2 | Sub-agent completes normally | Sub-agent result available |
| 3 | Sub-pipeline reaches its sensitive tool | HITL approval card appears (timing depends on mode — see behavior note above) |
| 4 | Verify card content | Card shows the correct pipeline sensitive tool name and arguments; card is attributed to the sub-pipeline |
| 5 | Click Approve | Sub-pipeline's sensitive tool executes; sub-pipeline completes |
| 6 | Observe parent synthesis | Parent response contains both sub-agent result and sub-pipeline result |

## Expected Final State

Sub-pipeline HITL card appeared correctly. After approval, both children completed. Parent synthesized both results.

## Pass/Fail Criteria

**Pass:**
- HITL card appears for the sub-pipeline's sensitive tool
- Card shows correct tool name and is attributed to the sub-pipeline (not the sub-agent)
- Approval routes to the correct child — sub-pipeline completes after approve
- Parent synthesizes both results

**Fail:**
- No HITL card appears (sub-pipeline sensitive tool executes without approval)
- Card misattributed to the sub-agent
- Approval doesn't resume the sub-pipeline
- Parent missing one or both results
