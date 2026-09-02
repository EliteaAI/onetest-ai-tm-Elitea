---
id: ELITEA-3137
title: "Mixed simultaneous interrupt types in one fan-out resolve independently without blocking each other"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3137: Mixed Simultaneous Interrupt Types Resolve Independently

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that when two children in the same fan-out hit *different* interrupt types at different times (e.g. one child hits a sensitive-tool approval, another later hits a toolkit-authorization prompt), both are tracked and resolvable independently and neither blocks the other.

## Preconditions

- New supervisor mode enabled
- Fan-out with at least two children: one configured to trigger a sensitive-tool approval, another configured to trigger a delegated-toolkit-authorization prompt, with staggered timing between them

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Send a prompt dispatching both children in parallel | Both children dispatched concurrently |
| 2 | Wait for the first child to hit its sensitive-tool approval | Its card appears independently (per ELITEA-3134), while the second child is still running |
| 3 | Wait for the second child to hit its toolkit-authorization prompt | Its card also appears independently, without displacing or blocking the first card |
| 4 | With both cards now visible, act on the second child's card first | Only the second child resumes; the first child's card remains visible and unresolved |
| 5 | Act on the first child's card | Only the first child resumes; both are now fully resolved |

## Expected Final State

Two different interrupt types coexist as independent, separately-resolvable cards regardless of resolution order.

## Pass/Fail Criteria

**Pass:** Both interrupt types surface and resolve independently, in either order, without one blocking or displacing the other.
**Fail:** Resolving one card affects, hides, or blocks the other; or the second interrupt type is delayed until the first is resolved.
