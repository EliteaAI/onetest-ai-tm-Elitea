---
id: ELITEA-3709
title: "Verify Preset Date Range Tabs Match Equivalent Manually-Entered Date Ranges"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6574]
---

# ELITEA-3709: Verify Preset Date Range Tabs Match Equivalent Manually-Entered Date Ranges

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify the preset range tabs (Today/Last 7d/Last 30d/Last 90d) produce identical totals to manually entering the equivalent From/To dates in the date picker.

**Coverage:**
- Numeric parity between preset tab totals/tables and the manually-entered equivalent range (distinct from ELITEA-3494, which only verifies the preset buttons set the correct From/To dates and visual active state, not data parity against a manual equivalent)

## Preconditions

- Access to Analytics with at least 7 days of usage history available

## Test Data

| Field | Value |
|-------|-------|
| Preset | "Last 7d" tab |
| Custom range | From/To dates manually set to the exact same 7-day window the preset represents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the "Last 7d" preset tab on Analytics | Totals and breakdown tables load for the preset range |
| 2 | Record Total Cost, Total Tokens, and all breakdown tables shown | Baseline recorded |
| 3 | Manually set the From/To date picker to the exact 7-day range the preset represents | Totals and breakdown tables reload for the manual range |
| 4 | Compare Total Cost, Total Tokens, and all breakdown tables against the step 2 baseline | All figures match exactly between the preset and the manually-entered equivalent range |

## Expected Final State

The preset tab and its manually-entered date-range equivalent produce identical Analytics figures.

## Pass/Fail Criteria

**Pass:**
- All totals and breakdown tables match exactly between the two methods

**Fail:**
- Any discrepancy exists between the preset tab and the equivalent manual range
