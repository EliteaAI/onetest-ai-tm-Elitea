---
id: ELITEA-3134
title: "Early independent HITL card renders near its own pause time, not delayed until siblings pause"
priority: critical
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, nfr:performance, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3134: Early Independent HITL Card Renders Near Its Own Pause Time

**Module:** Parallel Sub-Agent HITL · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in the new **single-process durable supervisor mode** (Track 3, per #6264), when one child of a parallel fan-out pauses for HITL well before its siblings, its interrupt card is rendered/persisted near its own pause time — not delayed until a sibling also pauses or finishes, as Track 1 (In-Process/aggregate) does today.

**Behavior note:** This supersedes the Track 1 aggregate wait documented in ELITEA-1720. Track 1/Track 2 behavior must remain unchanged when this new mode is disabled — see ELITEA-3140.

## Preconditions

- Logged in to {{base_url}}
- New supervisor mode enabled per dev-provided config (flag name/location TBD — confirm with dev at implementation time; feature is expected to ship gated off by default)
- Root agent fans out to at least two children with staggered completion times, e.g. a `Full Name Resolver`-style parent invoking a fast `Name Resolver` sub-agent and a slower `Surname Resolver` sub-agent, each configured to call a sensitive tool
- Ability to timestamp both the child's actual pause (e.g. via trace/log) and the card's appearance in the UI/network trace

## Test Data

| Field | Value |
|-------|-------|
| Fast child | e.g. Name Resolver — reaches sensitive tool quickly |
| Slow child | e.g. Surname Resolver — reaches sensitive tool noticeably later |
| Baseline for comparison | Track 1 aggregate delay observed in ELITEA-1720 (documented repro: ~17s) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Send a prompt dispatching both children in parallel under the new supervisor mode | Both children dispatched concurrently |
| 2 | Record the timestamp when the fast child actually pauses (reaches its sensitive tool / HITL point) | Timestamp captured from trace/log |
| 3 | Record the timestamp when the fast child's interrupt card appears in the chat UI | Timestamp captured from UI/network trace |
| 4 | Compute the gap between step 2 and step 3 | Gap is materially smaller than the Track 1 aggregate delay baseline — card appears at/near the child's own pause, not after the slow sibling |
| 5 | Confirm the slow child is still running (no card yet, active indicator visible) at the moment the fast child's card appears | Slow child's card has not appeared yet; its branch still shows active/running state |

## Expected Final State

The fast child's card is emitted independently and promptly at its own pause time, while the slow sibling continues running with its own card appearing later, independently.

## Pass/Fail Criteria

**Pass:**
- Fast child's card timestamp is close to its own pause timestamp (materially better than the Track 1 baseline gap)
- Slow child's card has not yet appeared while it's still running

**Fail:**
- Fast child's card is delayed until the slow sibling also pauses/finishes (Track 1 behavior reappearing under the new mode)
- Card timestamps cannot be distinguished from Track 1's aggregate-wait behavior
