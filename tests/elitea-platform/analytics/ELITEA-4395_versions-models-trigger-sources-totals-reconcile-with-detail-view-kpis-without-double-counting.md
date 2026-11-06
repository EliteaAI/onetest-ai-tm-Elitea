---
id: ELITEA-4395
title: "Versions, Models, and Trigger Sources totals reconcile with detail-view KPIs without double-counting, including Unknown rows"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, reconciliation]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4395: Versions, Models, and Trigger Sources totals reconcile with detail-view KPIs without double-counting, including Unknown rows

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that summing TOTAL TOKENS and COST across all Versions rows (including "Unknown version") and across all Trigger Sources rows (including "Unknown") each reconcile with the detail view's overall token/cost KPI totals for the same period, that Models' token/cost totals follow the same attribution scope as the detail-view totals (acknowledging RUNS may legitimately over-count), and that this reconciliation continues to hold after the date range is changed.

**Coverage:**
- Versions table token/cost sum reconciles with KPI totals (no double-counting)
- Trigger Sources table token/cost sum reconciles with KPI totals (no double-counting)
- Models table token/cost totals follow correct attribution scope (RUNS may over-count by design, tokens/cost must not double-count)
- Reconciliation holds across a date-range change

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with run history spanning multiple versions, models, and trigger sources, including at least one run with unknown version or trigger attribution if available
- Ability to read/export exact numeric values (not display-rounded) for comparison, or sufficiently precise on-screen values

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with multi-version, multi-model, multi-trigger run history |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and note the overall TOTAL TOKENS and COST KPI values for the current date range | KPI values recorded |
| 2 | Sum TOTAL TOKENS and COST across all rows in the Versions table, including any "Unknown version" row | Sum matches the KPI totals from step 1 (within acceptable rounding) |
| 3 | Sum TOTAL TOKENS and COST across all rows in the Trigger Sources table, including any "Unknown" row | Sum matches the KPI totals from step 1 (within acceptable rounding) |
| 4 | Sum TOTAL TOKENS and COST across all rows in the Models table | Sum follows the same attribution scope as the KPI totals — i.e., tokens/cost do not double-count even though RUNS may exceed total run count by design |
| 5 | Change the Analytics date range to a narrower or different window | All four tables and KPI cards refresh |
| 6 | Repeat steps 2–4 for the new date range | Reconciliation still holds for Versions, Trigger Sources, and Models under the new date range |

## Expected Final State

Versions and Trigger Sources token/cost sums exactly reconcile with the detail-view KPI totals (including Unknown rows) for any selected date range, and Models token/cost totals never double-count despite RUNS potentially exceeding total run count.

## Pass/Fail Criteria

**Pass:**
- Versions and Trigger Sources TOTAL TOKENS/COST sums equal the detail-view KPI totals, including Unknown rows
- Models TOTAL TOKENS/COST sums do not double-count tokens/cost (RUNS over-count is acceptable and expected)
- Reconciliation holds after changing the date range

**Fail:**
- Versions or Trigger Sources sums diverge from the KPI totals beyond rounding tolerance
- Models table shows inflated/double-counted tokens or cost
- Reconciliation breaks after a date-range change
