---
id: ELITEA-4124
title: "Verify multiple truncated agent cards expand independently without cross-contamination"
priority: medium
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least three published agents exist, each with a distinct, known welcome message exceeding the 8-line clamp

## Test Data

| Agent | Welcome message content |
|-------|--------------------------|
| Agent A | Distinct long text A |
| Agent B | Distinct long text B |
| Agent C | Distinct long text C |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Agents Studio and ensure Agent A, B, and C cards are visible on the same page | All three cards visible |
| 2 | Click "Show more" on Agent A's card | Expanded text matches Agent A's saved welcome message |
| 3 | Collapse Agent A's card | Card returns to clamped state |
| 4 | Click "Show more" on Agent B's card | Expanded text matches Agent B's saved welcome message, not Agent A's |
| 5 | Collapse Agent B's card | Card returns to clamped state |
| 6 | Click "Show more" on Agent C's card | Expanded text matches Agent C's saved welcome message |

## Expected Final State

Each card's expand/collapse behavior operates independently; no card ever displays another card's text.

## Pass/Fail Criteria

**Pass:**
- Each expansion shows only its own agent's correct, full text with no mixing or residual content from previously viewed cards

**Fail:**
- Any card shows text belonging to a different agent, or stale/residual text persists after switching between cards
