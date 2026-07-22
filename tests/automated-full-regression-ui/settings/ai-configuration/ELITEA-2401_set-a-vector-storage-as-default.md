---
id: ELITEA-2401
title: "Set a Vector Storage as default"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2401: Set a Vector Storage as default

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Set a Vector Storage as default. Success is confirmed when verify the selected card gains a "default" badge.

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
| 1 | Navigate to Settings → AI Configuration | Target page/section loads successfully. |
| 2 | Click the "Default vector storage" dropdown | Control responds; expected next state is shown. |
| 3 | Select a different vector storage configuration | Control responds; expected next state is shown. |
| 4 | Verify the dropdown updates to show the selected configuration | Condition holds as described. |
| 5 | Verify the selected card gains a "Default" badge | Condition holds as described. |

---

## Expected Final State

Verify the selected card gains a "Default" badge.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Set a Vector Storage as default.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
