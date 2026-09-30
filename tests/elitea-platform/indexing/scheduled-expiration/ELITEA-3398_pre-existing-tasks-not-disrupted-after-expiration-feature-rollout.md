---
id: ELITEA-3398
title: "Pre-existing scheduled indexing tasks are not unexpectedly disabled after expiration feature rollout"
priority: critical
type: regression
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to view scheduled indexing tasks
- At least one scheduled indexing task exists that was created before the expiration feature was deployed

## Test Data

| Field | Value |
|-------|-------|
| Legacy Task | Pre-existing scheduled task with no original expiration date |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Identify a pre-existing scheduled task created before the feature deployment | Task located; originally has no expiration date |
| 2 | Open the task after feature deployment | Task either has a retroactively assigned expiration date (per migration rule) or is exempted, per documented behavior |
| 3 | Verify the task's run status immediately after deployment | Task is not immediately/unexpectedly disabled |
| 4 | Continue observing the task through its next scheduled run(s) | Task continues running normally until any newly assigned expiration is reached |

## Expected Final State

Legacy tasks continue functioning without disruption immediately after rollout.

## Pass/Fail Criteria

**Pass:**
- No legacy task is unexpectedly disabled or loses data on rollout
- Legacy task behavior after deployment matches the documented migration rule

**Fail:**
- Any legacy task is immediately disabled, errors out, or loses configuration
- Legacy task's expiration handling is inconsistent or undocumented
