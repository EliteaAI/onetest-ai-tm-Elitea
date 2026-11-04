---
id: ELITEA-4427
title: "Verify empty state when no analytics data exists for run"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, empty-state, edge-case]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill run exists but has no usage_event data (edge case scenario)
- OR analytics endpoint returns empty result
- OR run failed before generating any analytics data

## Test Data

| Field | Value |
|-------|-------|
| Expected Message | "No analytics data is available for this run" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to analytics page for a run without data | Analytics page opens |
| 2 | Observe Costs tab | Empty state or zero values displayed |
| 3 | Check for empty state message | Message: "No analytics data is available for this run" |
| 4 | Navigate to Tokens tab | Empty state or zero values displayed |
| 5 | Navigate to Health tab | Empty state or no events shown |
| 6 | Verify no broken UI elements | UI remains stable |
| 7 | Verify no JavaScript errors in console | No console errors |
| 8 | Verify no broken charts or tables | UI components intact |
| 9 | Verify breadcrumbs and navigation still work | Navigation functional |
| 10 | Verify can navigate back to Run History | Back navigation works |

## Expected Final State

Empty state handling:
- Empty state message displayed: "No analytics data is available for this run"
- OR individual tabs show zero values with proper formatting
- No JavaScript errors
- No broken charts or tables
- UI remains stable and navigable
- Can navigate back to Run History

## Pass/Fail Criteria

**Pass:**
- Empty state message or zero values displayed
- Message is clear and informative
- No JavaScript errors
- No broken UI elements
- Navigation works correctly
- Page remains stable

**Fail:**
- No empty state handling
- Page crashes or shows error
- JavaScript errors in console
- Broken charts or tables
- Navigation broken
- UI unstable
