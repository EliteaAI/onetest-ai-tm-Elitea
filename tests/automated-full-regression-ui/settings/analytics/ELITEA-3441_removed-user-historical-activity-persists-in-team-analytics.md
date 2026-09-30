---
id: ELITEA-3441
title: "Removed User's Historical Activity Persists in Team Analytics"
priority: high
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [feat:monitoring, feat:roles-permissions, story:5110, regression, data-integrity]
requirements: [EliteaAI/elitea_issues#6796]
---
# ELITEA-3441: Removed User's Historical Activity Persists in Team Analytics

**Module:** Settings → Analytics · **Priority:** High · **Type:** Functional

**Objective:** Confirm that removing a user from a project, or changing their role, does not delete or hide their previously recorded historical activity on the Team Analytics → Activity tab — regression check for #6796. This is a data-loss bug, not just a cosmetic one: historical analytics data should be immutable with respect to later membership changes.

**Coverage:** Regression — [EliteaAI/elitea_issues#6796](https://github.com/EliteaAI/elitea_issues/issues/6796).

## Preconditions

- A project with Team Analytics enabled
- A user with existing recorded activity on that project, assigned a specific role

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the project's Team Analytics → Activity tab. | Activity data for the target user's role is visible for the relevant period. |
| 2 | Note the exact activity counts/entries attributable to the target user. | Baseline recorded for comparison. |
| 3 | Remove the target user from the project. | Removal succeeds. |
| 4 | Return to the Team Analytics → Activity tab and review the same period. | The user's previously recorded activity is still present and matches the step-2 baseline. |
| 5 | Repeat steps 1–4, but change the user's role instead of removing them. | Historical activity recorded under the user's prior role is still present and unchanged after the role change. |

## Expected Final State

Historical activity data recorded for the project persists regardless of later changes to user membership or role; removing/changing a user only affects their *future* activity attribution, never past records.

## Pass/Fail Criteria

**Pass:**
- Steps 4 and 5 both show the same activity data as the step-2 baseline

**Fail:**
- The removed or role-changed user's historical activity disappears or changes from the Activity tab after step 3 or its role-change variant
