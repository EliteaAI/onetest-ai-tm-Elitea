---
id: ELITEA-4339
title: "Verify skill usage and cost consistency between Usage page and Analytics page"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8, bug:7207]
requirements: [EliteaAI/elitea_issues#6929, EliteaAI/elitea_issues#7207]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one skill has been executed both as standalone run and as in-agent use
- Usage data exists for the selected date range

## Test Data

| Field | Value |
|-------|-------|
| Test Skill | Any skill with both standalone and in-agent usage |
| Date Range | Last 7 days |
| Usage Page URL | `{{base_url}}/usage` |
| Analytics Page URL | `{{base_url}}/settings/analytics?tab=skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/usage` | Usage page loads with "Top skills" widget visible |
| 2 | Set date range to "Last 7 days" using date picker | Date range updates to Last 7 days |
| 3 | Locate the "Top skills" widget and identify a skill with non-zero usage | Skill is visible with Uses and Spend values displayed |
| 4 | Record the skill name, "Uses" count, and "Spend" value from Usage page | Values recorded (e.g., skill-name: Uses=5, Spend=$0.0025) |
| 5 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 6 | Ensure the same date range (Last 7 days) is selected | Date range matches "Last 7 days" |
| 7 | Locate the same skill in the "Skill Activity" table | Skill found in table |
| 8 | Record "Runs", "Agent & Chat Uses", and "Cost" values for the skill | Values recorded (e.g., Runs=2, Agent & Chat Uses=3, Cost=$0.0025) |
| 9 | Compare Usage page "Uses" with Analytics page "Runs" | Usage page "Uses" equals Analytics "Runs" (standalone runs only) |
| 10 | Compare Usage page "Spend" with Analytics page "Cost" | Values match exactly to the same decimal precision ($0.0025 = $0.0025) |
| 11 | Calculate total invocations: Analytics Runs + Agent & Chat Uses | Total = 2 + 3 = 5 invocations |
| 12 | Verify total matches context (if Usage "Uses" meant total, or just standalone) | Clarify if Usage "Uses" = standalone only or total (per issue #7207, Usage shows standalone only) |

## Expected Final State

- Usage page "Uses" count matches Analytics page "Runs" count (standalone executions only)
- Usage page "Spend" matches Analytics page "Cost" to displayed precision
- Agent & Chat Uses are tracked separately in Analytics and not included in Usage page "Uses"
- No discrepancy between the two pages for the same skill and date range

## Pass/Fail Criteria

**Pass:**
- Usage page "Uses" = Analytics page "Runs" for standalone executions
- Usage page "Spend" = Analytics page "Cost" (exact match to displayed precision)
- Agent & Chat Uses displayed separately in Analytics, not double-counted in "Uses"
- Consistency maintained across both pages for the same date range

**Fail:**
- Usage page "Uses" ≠ Analytics page "Runs"
- Usage page "Spend" ≠ Analytics page "Cost"
- Mismatch in values between the two pages
- Agent & Chat Uses incorrectly included or excluded from totals
