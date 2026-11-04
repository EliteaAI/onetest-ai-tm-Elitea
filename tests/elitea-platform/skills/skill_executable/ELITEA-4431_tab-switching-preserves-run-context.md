---
id: ELITEA-4431
title: "Verify tab switching preserves run context across all tabs"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, state-management, tabs]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has data for all tabs

## Test Data

| Field | Value |
|-------|-------|
| Tabs to Test | Costs, Tokens, Health (and Tools if visible) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On analytics page, note run's metadata from header | Date, version, model recorded |
| 2 | Click "Costs" tab | Costs tab active |
| 3 | Verify data displays | Cost data shown |
| 4 | Note TOTAL COST value | Value recorded |
| 5 | Click "Tokens" tab | Tokens tab active |
| 6 | Verify data displays | Token data shown |
| 7 | Note TOTAL TOKENS value | Value recorded |
| 8 | Verify run metadata unchanged in header | Same date, version, model |
| 9 | Click "Health" tab | Health tab active |
| 10 | Verify data displays | Health data shown |
| 11 | Verify run metadata unchanged | Same date, version, model |
| 12 | (If visible) Click "Tools" tab | Tools tab active |
| 13 | Verify data displays | Tool data shown (if tab exists) |
| 14 | Verify run metadata unchanged | Same date, version, model |
| 15 | Return to "Costs" tab | Costs tab active again |
| 16 | Verify TOTAL COST matches previously noted value | Same value displayed |
| 17 | Verify run metadata still unchanged | Same date, version, model throughout |
| 18 | Verify no cross-contamination from other runs | All data consistent for ONE run |

## Expected Final State

Tab switching behavior:
- All tabs switch smoothly without page reload
- Run metadata (header) remains consistent across all tabs
- Each tab displays data for the SAME run
- No cross-contamination from other runs
- Tab selection state maintained per user action
- Data values remain consistent

## Pass/Fail Criteria

**Pass:**
- Tabs switch smoothly
- Run metadata unchanged throughout
- All data from same run
- No cross-run contamination
- Values consistent across tab switches
- No navigation errors

**Fail:**
- Tab switching broken or causes reload
- Run metadata changes between tabs
- Data from different runs appears
- Cross-contamination detected
- Values change unexpectedly
- Navigation errors
