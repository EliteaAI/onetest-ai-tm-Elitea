---
id: ELITEA-4430
title: "Verify browser refresh preserves selected run context"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, state-management, navigation]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has specific identifiable metadata (date, version, model)

## Test Data

| Field | Value |
|-------|-------|
| Refresh Method | F5, Ctrl+R, or browser refresh button |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to analytics page for a specific run | Analytics page displays |
| 2 | Note current run's metadata: date, version, model | Metadata recorded |
| 3 | Note current total cost and tokens | Values recorded |
| 4 | Select a specific tab (e.g., Tokens) | Tokens tab active |
| 5 | Press F5 or Ctrl+R to refresh browser | Page refresh initiates |
| 6 | Wait for page reload | Page reloads |
| 7 | Verify same run's data is displayed | Same run metadata shown |
| 8 | Verify date, version, model unchanged | Metadata matches recorded values |
| 9 | Verify cost and tokens match previous values | Same run data displayed |
| 10 | Verify URL remains unchanged | URL identical to before refresh |
| 11 | Note which tab is active (may reset to Costs - acceptable) | Tab state observed |
| 12 | Verify no data from different runs appears | No cross-run contamination |
| 13 | Verify no navigation errors or redirect | Stays on analytics page |

## Expected Final State

After browser refresh:
- Page reloads successfully
- Same run's data displayed (same date, version, model)
- URL unchanged
- Run context maintained
- Previously selected tab may reset to default (Costs) - acceptable behavior
- No data from different runs
- No navigation errors

## Pass/Fail Criteria

**Pass:**
- Page reloads without errors
- Same run data displayed
- Metadata unchanged
- URL preserved
- No cross-run data contamination
- Navigation stable

**Fail:**
- Page fails to reload
- Different run data displayed
- Metadata changed
- URL changed or broken
- Data from different runs appears
- Navigation errors or redirect to wrong page
