---
id: ELITEA-3144
title: "[NEEDS DEV FIXTURE] Crash between early-card emission and sibling settlement, and Redis/pub-sub outage, both degrade gracefully without losing or duplicating decisions"
priority: medium
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, nfr:performance, r-2.0.6, issue:6264, blocked]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3144: Crash Recovery and Redis Outage Degrade Gracefully

**Module:** Parallel Sub-Agent HITL · **Priority:** Medium · **Type:** Functional

**Objective:** Verify two durability scenarios from #6264: (1) a worker crash/restart occurring between an early card's emission and its siblings settling does not lose or duplicate the card/decision on recovery; (2) a Redis/pub-sub outage during a fan-out causes graceful degradation to the existing durable aggregate-interrupt flow rather than losing the interrupt.

**Fixture note:** Both scenarios require a dev-provided way to trigger a worker crash/restart and a Redis/pub-sub outage at a precise point in the fan-out lifecycle — not achievable as a normal black-box QA action in staging. This test is blocked pending that fixture; do not attempt to simulate a crash by killing arbitrary processes in a shared staging environment.

## Preconditions

- New supervisor mode enabled
- Dev-provided fault-injection fixture available to: (a) crash/restart the worker process at a controlled point between an early card's emission and sibling settlement; (b) make Redis/pub-sub unavailable during an active fan-out
- Staggered fan-out scenario as used in ELITEA-3134

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Start a staggered fan-out; wait until the fast child's card has been emitted while the slow sibling is still running | Fast child's card visible; slow sibling still running |
| 2 | Using the dev fixture, crash/restart the worker process at this point | Worker recovers; exactly one root supervisor resumes (not one process forked per child) |
| 3 | After recovery, inspect the fast child's card/decision state | Not lost, not duplicated; if a decision was already made before the crash, it is preserved; if not, the card is still resolvable exactly once |
| 4 | Resolve the fast child's card post-recovery and confirm the slow sibling proceeds correctly to its own independent pause/settlement | Behaves as if no crash had occurred, from a user-observable standpoint |
| 5 | Repeat with the Redis/pub-sub outage fixture instead of a worker crash, during an active fan-out | The flow degrades to the existing durable aggregate-interrupt behavior (per Track 1) rather than losing the interrupt entirely |

## Expected Final State

Both fault scenarios are absorbed without data loss or duplication, and recovery/degradation is observable as correct end-user behavior (card still resolvable, no duplicate execution, no lost interrupt).

## Pass/Fail Criteria

**Pass:** Crash recovery preserves/does not duplicate the decision and resumes cleanly; Redis outage degrades to the aggregate flow without losing the interrupt.
**Fail:** A decision or card is lost or duplicated after crash recovery; an interrupt is silently lost during a Redis/pub-sub outage.

## Blocked / Fixture Needed

Blocked pending a dev-provided fault-injection fixture for both the worker crash/restart and the Redis/pub-sub outage scenarios. Not executable as an unaided black-box QA action.
