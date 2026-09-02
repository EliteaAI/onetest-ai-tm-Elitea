---
id: ELITEA-3143
title: "Regenerate retires the entire prior fan-out generation without resurrecting or duplicating old independent cards"
priority: high
type: functional
module: parallel-subagent-hitl
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, issue:6264]
requirements: [EliteaAI/elitea_issues#6264]
---
# ELITEA-3143: Regenerate Retires the Entire Prior Generation

**Module:** Parallel Sub-Agent HITL · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Regenerate after a fan-out (with some early independent cards already resolved and possibly one still pending) fully retires the prior generation — old independent cards from the retired generation do not resurface or duplicate in the new generation.

## Preconditions

- New supervisor mode enabled
- A completed or partially-resolved staggered fan-out available to regenerate from (e.g. fast child's card already resolved, slow child's card resolved or still pending)

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Complete or partially resolve a staggered fan-out (at least one card already acted on) | Prior generation's cards are in their resolved/pending state |
| 2 | Click Regenerate on the response | A new generation begins |
| 3 | Observe the new generation's fan-out as it re-runs | New independent cards (if any) appear fresh for the new generation, correctly attributed to the new generation |
| 4 | Confirm no card from the retired (prior) generation reappears or is duplicated into the new generation | Old generation's cards do not resurface, regardless of whether the old fan-out had card(s) still pending at the time of regenerate |
| 5 | If the prior generation had a still-pending card at the moment Regenerate was clicked, confirm that pending interrupt is fully retired (not still actionable, and its underlying child is not still running in the background) | Prior pending card/branch is retired along with the rest of the old generation |

## Expected Final State

The new generation's independent cards are entirely its own; no cross-generation duplication or resurfacing occurs.

## Pass/Fail Criteria

**Pass:** No old-generation card reappears/duplicates after Regenerate; any old still-pending interrupt is fully retired.
**Fail:** An old card resurfaces or duplicates in the new generation, or an old pending child continues running/actionable after Regenerate.
