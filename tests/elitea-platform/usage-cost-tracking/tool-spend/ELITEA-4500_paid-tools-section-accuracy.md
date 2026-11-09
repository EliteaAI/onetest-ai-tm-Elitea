---
id: ELITEA-4500
title: "Paid Tools section on Usage page accurately reflects spend, limit, and call count"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4500: Paid Tools section on Usage page accurately reflects spend, limit, and call count

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Confirm the "Paid Tools" block on Settings → Usage shows a correct dollar amount, limit, and call count for a feature as real usage accumulates.

**Coverage:**
- Call count and $ spent update correctly per call
- Progress bar reflects updated percentage
- "$X of $Y" formatting remains consistent

## Preconditions

- Project has the paid-tool module (e.g. Web Search) enabled with a known, non-zero monthly limit configured

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |
| Example calls to trigger | 3 web searches |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → Usage, note current Paid Tools line (e.g. "Web search: $X of $Y", call count, progress bar %). | Baseline values recorded. |
| 2 | Trigger a known number of qualifying tool calls (e.g. 3 web searches) via chat. | Calls succeed. |
| 3 | Refresh Settings → Usage. | Call count increased by the expected amount; $ spent increased consistent with per-call cost. |
| 4 | Observe the progress bar. | Progress bar visually reflects the updated percentage. |
| 5 | Check the displayed format. | "$0.07 of $7.00"-style format remains consistent (two decimal places, correct currency symbol). |

## Expected Final State

Paid Tools section accurately and consistently reflects real usage after each qualifying call.

## Pass/Fail Criteria

**Pass:**
- Call count and $ spent update correctly and consistently per call
- Formatting remains consistent

**Fail:**
- Call count or $ spent fails to update correctly, or formatting is inconsistent
