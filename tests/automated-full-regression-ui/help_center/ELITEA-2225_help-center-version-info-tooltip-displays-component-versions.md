---
id: ELITEA-2225
title: "Help Center — version info tooltip displays component versions and can be copied"
priority: high
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2225: Help Center — version info tooltip displays component versions and can be copied

**Module:** help-center · **Priority:** high · **Type:** functional

**Objective:** Verify that Help Center — version info tooltip displays component versions and can be copied. Success is confirmed when paste the clipboard contents into a text editor and verify all component version details are included.

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
| 1 | Navigate to Help Center | Target page/section loads successfully. |
| 2 | Locate the version label in the top right corner (e.g., "Version: 2.0.3 (28-May-2026)") | Action completes without error and produces the expected UI state. |
| 3 | Click the "i" (info) icon next to the version label | Control responds; expected next state is shown. |
| 4 | Verify a tooltip/dropdown appears showing detailed component versions: elitea_core, admin, notifications, configurations, sdk_plugin, indexer_worker | Condition holds as described. |
| 5 | Verify each component shows its version number | Condition holds as described. |
| 6 | Verify a copy icon is present at the bottom of the tooltip | Condition holds as described. |
| 7 | Click the copy icon | Control responds; expected next state is shown. |
| 8 | Verify a success notification appears (e.g., "Copied to clipboard") | Condition holds as described. |
| 9 | Paste the clipboard contents into a text editor and verify all component version details are included | Field accepts the input and displays the entered value. |

---

## Expected Final State

Paste the clipboard contents into a text editor and verify all component version details are included.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — version info tooltip displays component versions and can be copied.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
