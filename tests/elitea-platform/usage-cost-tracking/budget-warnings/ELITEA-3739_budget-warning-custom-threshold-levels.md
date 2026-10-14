---
id: ELITEA-3739
title: "Budget Warnings — Custom Warning Threshold Changes the First Level and Re-Evaluates Stored Dismissals"
priority: medium
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3739: Budget Warnings — Custom Warning Threshold Changes the First Level and Re-Evaluates Stored Dismissals

**Module:** Usage Cost Tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the first warning level follows the configured threshold per scope, that the fixed 90/95 levels apply only above it, and that changing the threshold re-evaluates an existing dismissal.

**Coverage:**
- Threshold variants 50 / 92 / 97 / 100
- Personal project uses the personal project threshold
- Lowering / raising the threshold while a dismissal is stored

## Preconditions

- Admin access to Admin → Features → Cost Budgets (warning thresholds); Cost Budgets mode = **enforce**
- A test user with a small member limit in a team project, and a personal project with a small limit
- Note: the issue describes a fixed first alert at 80%. The implementation uses the configured threshold (expected behavior)

## Test Data

| Threshold | Spend checks | Expected levels |
|-----------|--------------|-----------------|
| 50 | 49%, 60%, 91%, 96% | none → 50 → 90 → 95 |
| 92 | 91%, 93%, 96% | none → 92 (elevated) → 95; 90 never appears |
| 97 | 96%, 98% | none → 97 (critical); only one level |
| 100 | any % | never a banner |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For each threshold in Test Data, set the per-member warning threshold, save, and check the banner and API at each listed spend % (reload ~60s after spending) | `level` and severity match the table |
| 2 | In the personal project, set the personal project threshold to a value different from the team one (e.g. 60) and check at ~65% | Banner appears at level 60, so the personal threshold is used |
| 3 | Threshold 80, spend ~75%, with a stored dismissal of `80` for this month: lower the threshold to **70** | Banner stays hidden (level 70 < stored 80) |
| 4 | Threshold 80, dismissed at 80, spend ~86%: raise the threshold to **85** | Banner **shows** again at level 85 (85 > stored 80) |

## Expected Final State

Levels always follow the configured threshold.

## Teardown

- Reset all warning thresholds to 80

## Pass/Fail Criteria

**Pass:**
- Levels match the table for every threshold
- Personal projects use the personal threshold
- Threshold changes re-evaluate dismissals as described

**Fail:**
- First level fixed at 80 regardless of configuration
- 90 shown as a level when the threshold is above 90, or a banner at threshold 100
