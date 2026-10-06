---
id: ELITEA-2314
title: "Predefined date presets update the From/To pickers and refresh all content"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2314: Predefined date presets update the From/To pickers and refresh all content

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Predefined date presets update the From/To pickers and refresh all content. Success is confirmed when verify only one preset is highlighted at a time.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics | Target page/section loads successfully. |
| 2 | Verify "Last 7d" is active by default and From/To reflect a 7-day range | Condition holds as described. |
| 3 | Click "Last 24h" — verify the button highlights, From/To update to a 24h range, data refreshes | Control responds; expected next state is shown. |
| 4 | Click "Last 30d" — verify From/To update to a 30-day range, data refreshes | Control responds; expected next state is shown. |
| 5 | Click "Last 90d" — verify From/To update to a 90-day range, data refreshes | Control responds; expected next state is shown. |
| 6 | Verify only one preset is highlighted at a time | Condition holds as described. |

---

## Expected Final State

Verify only one preset is highlighted at a time.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Predefined date presets update the From/To pickers and refresh all content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
