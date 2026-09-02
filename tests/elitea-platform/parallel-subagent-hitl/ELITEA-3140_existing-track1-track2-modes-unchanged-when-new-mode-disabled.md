---
id: ELITEA-3140
title: "Existing Track 1 (aggregate) and Track 2 (Park+Dispatch) modes remain unchanged when the new supervisor mode is disabled"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3140: Existing Track 1 / Track 2 Modes Remain Unchanged (Regression)

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that the new single-process durable supervisor mode (#6264) is feature-gated, and that with the gate off, today's two existing modes — Track 1 In-Process aggregate wait, and Track 2 Park+Dispatch (`parallel_subagent_dispatch: true`) — behave exactly as before the change.

**Behavior note:** This is the regression backstop for ELITEA-1720/1721 (Track 1) and their Track 2 equivalents — this new feature must not alter their behavior when disabled.

## Preconditions

- New supervisor mode's feature gate is present and can be explicitly set to disabled/off
- Ability to run the same staggered two-sub-agent scenario used in ELITEA-1720/1721

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | With the new supervisor mode explicitly disabled and `parallel_subagent_dispatch` absent/false (Track 1), repeat the ELITEA-1720 scenario | No card appears while a sibling is still running; both cards appear together only once both children pause (unchanged aggregate behavior) |
| 2 | Repeat the ELITEA-1721 scenario (approve one, reject other) under the same Track 1 settings | Execution resumes only after ALL cards are resolved, exactly as ELITEA-1721 describes — no early independent resume |
| 3 | With the new supervisor mode disabled and `parallel_subagent_dispatch: true` (Track 2), repeat a staggered two-sub-agent scenario | Each child dispatches to its own process (Track 2 semantics) exactly as before this change, unaffected by the new mode's code paths |
| 4 | Confirm the feature-gate toggle itself is visible/settable by an admin (location per dev documentation once shipped) | Toggle exists and defaults to off/disabled |

## Expected Final State

With the gate off, Track 1 and Track 2 are byte-for-byte behaviorally identical to their pre-#6264 behavior.

## Pass/Fail Criteria

**Pass:** Track 1 and Track 2 behave identically to ELITEA-1720/1721 and pre-existing Track 2 behavior when the new mode is disabled.
**Fail:** Any observable change to Track 1 or Track 2 behavior occurs merely from the new mode's code being present, even while disabled.
