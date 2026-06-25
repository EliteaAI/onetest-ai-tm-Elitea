---
id: ELITEA-1730
title: "Sequential sub-agent HITL resume does not re-invoke the already-completed first sub-agent"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4993]
---
# ELITEA-1730: Sequential Sub-Agents — HITL Resume Does Not Re-Invoke First

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a second sequential sub-agent triggers HITL and the user approves, the first (already completed) sub-agent is not re-invoked — the normalization fix from PR #199.

**Applies to:** Mode-agnostic — sequential sub-agent calls (not parallel fan-out). The parent calls A then B in sequence, not concurrently.

## Preconditions

- Logged in to {{base_url}}
- Parent agent calls Sub-Agent A (safe, no sensitive tools) then Sub-Agent B (has sensitive tool) **sequentially** (not in parallel)

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a prompt triggering Sub-Agent A then Sub-Agent B | Sub-Agent A dispatched first |
| 2 | Sub-Agent A completes | Sub-Agent A result in parent's context |
| 3 | Execution pauses at Sub-Agent B's sensitive tool | Approval card names **Sub-Agent B's tool** (not Sub-Agent A) |
| 4 | Click Approve | Sub-Agent B resumes |
| 5 | Observe Sub-Agent A during/after resume | Sub-Agent A NOT re-invoked; prior result unchanged |
| 6 | Observe parent final output | Contains both results exactly once |

## Expected Final State

Sub-Agent A ran once before pause. Sub-Agent B resumed and completed. Parent has both results exactly once.

## Pass/Fail Criteria

**Pass:**
- Approval card names Sub-Agent B's tool
- Sub-Agent A not re-invoked on resume
- Parent output has both results exactly once

**Fail:**
- Sub-Agent A re-invoked (duplicate side effects)
- Wrong tool name on card
- Missing or duplicated results
