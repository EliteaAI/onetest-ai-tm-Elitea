---
id: ELITEA-3622
title: "Regression - Run History Functionality"
priority: high
type: regression
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:agents, feat:pipelines, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3622: Regression - Run History Functionality

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Run History panel and existing functionality is not affected by Analytics addition.

## Preconditions

- Logged into {{base_url}}
- Agent with multiple prior runs exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an Agent with prior runs. | Agent page loads. |
| 2 | Verify history icon button is visible. | History/clock icon present. |
| 3 | Click history icon. | Run History panel opens. |
| 4 | Verify panel title is "Run History". | Title unchanged. |
| 5 | Verify table has 3 columns: Date, Version, Duration. | Columns unchanged. |
| 6 | Verify "Restore chat" option works. | Click restores conversation to chat. |
| 7 | Click X button to close panel. | Panel closes correctly. |
| 8 | Re-open and close panel multiple times. | Works consistently. |

## Pass/Fail Criteria

**Pass:** Run History panel works as before, Restore chat functional, panel open/close works.
**Fail:** Panel broken, columns changed, or existing functionality affected.
