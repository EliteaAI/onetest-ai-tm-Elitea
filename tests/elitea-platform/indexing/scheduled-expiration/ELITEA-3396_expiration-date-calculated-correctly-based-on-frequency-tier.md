---
id: ELITEA-3396
title: "Expiration date is calculated correctly based on scheduled indexing task frequency tier"
priority: critical
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to create scheduled indexing tasks
- A Datasource/Artifact source is available to index

## Test Data

| Frequency | Expected Expiration Rule |
|-----------|---------------------------|
| Daily | 90 days from creation |
| Weekly (<1 month interval) | 90 days from creation |
| Monthly | 180 days from creation (or 6x task duration if greater) |
| Every 2 months | 6x task duration if it exceeds 180 days, else 180 days |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a scheduled indexing task with Daily frequency | Task created; stored expiration date = creation date + 90 days |
| 2 | Create a scheduled indexing task with Weekly frequency | Task created; stored expiration date = creation date + 90 days |
| 3 | Create a scheduled indexing task with Monthly frequency | Task created; stored expiration date = creation date + 180 days |
| 4 | Create a scheduled indexing task with a 2-month interval | Task created; expiration date follows the 6x-duration-or-180-day rule, whichever is greater |
| 5 | Open each task's detail view and inspect the expiration date field | Displayed expiration date matches the value calculated per the frequency-tier rule for each task |

## Expected Final State

Each task has a stored, correctly-calculated expiration date matching its frequency tier.

## Pass/Fail Criteria

**Pass:**
- All four tasks show expiration dates matching the documented tier rules
- Expiration date field is populated for every task

**Fail:**
- Any task's expiration date is missing, null, or miscalculated
- Expiration date does not follow the documented tiering rule
