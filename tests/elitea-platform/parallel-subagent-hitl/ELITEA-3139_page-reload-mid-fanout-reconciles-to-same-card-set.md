---
id: ELITEA-3139
title: "Page reload mid-fan-out reconciles to the same independent card set and identities as the live view"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3139: Page Reload Mid-Fan-Out Reconciles Correctly

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that reloading the page while a fan-out is mid-flight (some children paused on independent cards, some still running) reconciles to the same set of cards, with the same identities, as the live view before reload.

## Preconditions

- New supervisor mode enabled
- A staggered fan-out with at least one child already paused on an independent card and at least one sibling still running at the moment of reload

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Dispatch a staggered fan-out; wait until one child's card is visible while a sibling is still running | Live state: one card visible, one branch still running |
| 2 | Reload the page | Page reloads and re-fetches conversation state |
| 3 | Compare the reloaded view's card(s) to the live view from step 1 | Same card(s) present, same identity (same child/branch attribution), no duplicates, none missing |
| 4 | Act on the reloaded card | Behaves identically to acting on it live — resumes only that child, removes only that card |
| 5 | If the sibling has since also paused, confirm its card appears correctly post-reload as well | Sibling's card (if now paused) is present and correctly attributed after reload |

## Expected Final State

The reloaded view is fully consistent with the live view's card set and identities, and remains fully functional for resolving remaining interrupts.

## Pass/Fail Criteria

**Pass:** No duplicate cards, no missing cards, and no misattribution after reload; acting on a reloaded card works exactly as it would live.
**Fail:** A card is duplicated, lost, or misattributed after reload; or acting on a reloaded card behaves differently than live (e.g. affects a sibling, fails to resume).
