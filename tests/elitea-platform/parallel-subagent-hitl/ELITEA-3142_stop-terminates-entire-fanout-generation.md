---
id: ELITEA-3142
title: "Stop terminates the entire fan-out generation, not just the visible/active branch"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3142: Stop Terminates the Entire Fan-Out Generation

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Stop during an active fan-out (with at least one child already paused on an independent card and at least one sibling still running) terminates the entire generation — not just the currently visible/active branch — leaving no orphaned running children and no stray cards.

## Preconditions

- New supervisor mode enabled
- Staggered fan-out with one child's card visible and a sibling still actively running

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Dispatch the staggered fan-out; wait until one child's card is visible while the sibling is still running | Live state: one card visible, one branch running |
| 2 | Click Stop | The entire generation is terminated |
| 3 | Observe the previously-running sibling branch | No longer executing; does not continue to run in the background |
| 4 | Observe the previously-visible card | Removed/invalidated — cannot be acted on after Stop |
| 5 | Check for any stray cards or orphaned running state after a short wait | None — no child continues executing, no interrupt card remains actionable |
| 6 | Send a new message in the same conversation | New generation starts cleanly, unaffected by the stopped generation's state |

## Expected Final State

Stop fully terminates every branch of the fan-out, including already-paused and still-running children, with no residual state.

## Pass/Fail Criteria

**Pass:** All branches (paused and running) are terminated by Stop; no card remains actionable; no orphaned execution continues.
**Fail:** A sibling branch continues running after Stop, or a previously-shown card remains actionable and can still be resolved after Stop.
