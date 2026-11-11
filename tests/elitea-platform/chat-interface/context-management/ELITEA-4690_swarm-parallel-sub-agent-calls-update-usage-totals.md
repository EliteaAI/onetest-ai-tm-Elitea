---
id: ELITEA-4690
title: "Swarm Parallel Sub-Agent Calls Update Usage Totals Atomically"
priority: medium
type: integration
module: context-management
status: draft
execution_type: manual
regression: false
tags: [feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

## Scope Note

Kept as a manual spot-check only — timing-dependent and not suitable as a reliable repeatable regression gate.

## Preconditions

- Swarm mode is enabled and a chat with two or more sub-agents capable of running in parallel is available

## Test Data

| Field | Value |
|-------|-------|
| Swarm-capable chat | Chat configured with 2+ sub-agents that can run in parallel within one turn |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the current Usage totals (Input/Output tokens, cost) before the run. | Baseline recorded. |
| 2 | Trigger a swarm-mode run where two or more sub-agents execute in parallel as part of a single turn. | All sub-agents complete their parallel execution; the run finishes. |
| 3 | Note the final Usage totals after the run completes. | Final values recorded. |
| 4 | Independently estimate the expected total based on the number of parallel sub-agent calls and their approximate response sizes. | An expected total/range is calculated. |
| 5 | Compare the displayed final Usage totals against the independently estimated expectation. | The displayed totals are consistent with ALL parallel calls being counted — not just one call (undercounting) and not duplicated (double-counting). |

## Expected Final State

Usage totals correctly and atomically reflect every parallel sub-agent call from a single swarm turn, with no lost or duplicated updates.

## Pass/Fail Criteria

**Pass:**
- Final Usage totals are consistent with all parallel sub-agent calls being counted exactly once each

**Fail:**
- Usage totals reflect fewer calls than actually ran (lost updates from concurrent writes)
- Usage totals reflect more than the actual number of calls (duplicated counting)
