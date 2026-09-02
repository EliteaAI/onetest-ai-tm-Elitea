---
id: ELITEA-3135
title: "Resuming an early independent card affects only that child; card is removed immediately; no duplicate execution"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3135: Resuming an Early Card Only Affects That Child

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that under the new supervisor mode (Track 3, #6264), acting (approve/reject) on one child's early independent card resumes only that child — siblings that are still running or still paused remain untouched — and the acted-on card disappears immediately without leaving a duplicate interrupt or triggering duplicate tool execution.

## Preconditions

- Same staggered fan-out setup as ELITEA-3134, with the fast child's card already visible while the slow sibling is still running (or itself now also paused)
- Ability to observe each child's execution/tool-call state independently (trace, logs, or per-branch UI activity indicator)

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | With the fast child's card visible and the slow sibling still running, click Approve (or Reject) on the fast child's card | Only the fast child resumes; the slow sibling's execution is unaffected and continues independently |
| 2 | Observe the fast child's card immediately after the action | Card disappears immediately |
| 3 | Observe the slow sibling's branch | Still shows its own active/running (or independently paused) state, unaffected by the action taken on the fast child's card |
| 4 | Confirm the fast child's tool executes exactly once following approval (or does not execute at all following rejection) | No duplicate execution; no duplicate interrupt reappears for the same pause |
| 5 | Wait for the slow sibling to reach its own pause point | Slow sibling surfaces its own independent card, unaffected by the earlier action |

## Expected Final State

Acting on one child's card is fully isolated to that child: immediate card removal, exactly one resulting execution outcome (or none, on rejection), and no effect on sibling branches.

## Pass/Fail Criteria

**Pass:**
- Only the acted-on child resumes; siblings are unaffected
- The acted-on card disappears immediately
- No duplicate tool execution or duplicate interrupt for the acted-on child

**Fail:**
- Acting on one card affects or resumes a sibling
- The card lingers after being acted on
- The child's tool executes more than once, or the interrupt reappears after being resolved
