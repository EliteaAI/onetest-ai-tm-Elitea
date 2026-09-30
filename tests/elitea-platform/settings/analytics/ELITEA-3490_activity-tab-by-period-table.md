---
id: ELITEA-3490
title: "Activity Tab Activity by Period Table"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3490: Activity Tab Activity by Period Table

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Activity by Period table displays correct daily/weekly/monthly breakdown.

## Preconditions

- Logged into {{base_url}}
- Project has activity data
- Navigate to Settings → Analytics → Activity

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Activity by Period" section. | Table visible below the chart. |
| 2 | Verify table columns. | Columns: PERIOD, ACTIVE USERS, AI ACTIVE USERS. |
| 3 | Verify PERIOD format matches toggle. | Shows dates in Day view (e.g., "Sep 29, 2026"). |
| 4 | Verify ACTIVE USERS count. | Integer count of distinct active users per period. |
| 5 | Verify AI ACTIVE USERS count. | Integer count of users who triggered AI features. |
| 6 | Change to Week toggle. | Period column shows week ranges. |
| 7 | Verify AI ACTIVE ≤ ACTIVE for each row. | AI Active count never exceeds total Active Users. |

## Pass/Fail Criteria

**Pass:** Table shows correct period format, counts are logical, toggles update table.
**Fail:** Period format wrong, counts inconsistent, or toggle doesn't update table.
