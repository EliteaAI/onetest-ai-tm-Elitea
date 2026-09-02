---
id: ELITEA-3138
title: "Independent card attribution and per-branch activity indicators are correct in nested fan-out hierarchies"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3138: Card Attribution and Activity Indicators Are Correct in Nested Hierarchies

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that in a nested fan-out (root → mid-level agent → leaf resolver), each independent early card is attributed to the correct `parent_agent_path`, and the running/shimmer activity indicator appears only on branches that are actually still executing.

## Preconditions

- New supervisor mode enabled
- A nested fan-out at least two levels deep, e.g. root agent → `Full Name Resolver` (mid-level) → `Name Resolver` + `Surname Resolver` (leaves), with staggered pause times among the leaves
- At least two `Full Name Resolver`-style branches running in parallel at the root, each with its own leaf children, so branch attribution can be cross-checked

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Dispatch the nested, multi-branch fan-out | Multiple branches and their nested children begin executing |
| 2 | Observe each independent card as leaf children pause at different times | Each card's displayed context/path correctly reflects its own branch and nesting level — not flattened to the root, not attributed to a sibling branch or a different parent |
| 3 | Observe the activity/shimmer indicator on each branch while some leaves are paused and others still running | Only branches with children still actively executing show the running/shimmer indicator; paused or already-resolved branches do not |
| 4 | Resolve one leaf's card | That leaf's branch indicator stops (or reflects the new state); sibling branches' indicators remain accurate to their own state |

## Expected Final State

Every card and activity indicator accurately reflects its own branch's real-time state and nesting, with no cross-branch bleed.

## Pass/Fail Criteria

**Pass:** Card attribution and activity indicators are correct per-branch throughout the fan-out, including after partial resolution.
**Fail:** A card is attributed to the wrong branch/parent, or an activity indicator shows "running" for a branch that is paused/resolved (or vice versa).
