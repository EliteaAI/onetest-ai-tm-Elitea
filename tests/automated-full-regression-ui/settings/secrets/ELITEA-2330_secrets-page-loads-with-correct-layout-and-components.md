---
id: ELITEA-2330
title: "Secrets page loads with correct layout and components"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2330: Secrets page loads with correct layout and components

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Secrets page loads with correct layout and components. Success is confirmed when verify pagination controls are shown: rows per page selector, page range label (e.g., "1–10 of 15"), prev/next arrows.

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
| 1 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 2 | Verify the page header shows "Secrets" | Condition holds as described. |
| 3 | Verify a Search input is present in the top right | Condition holds as described. |
| 4 | Verify a "+" button is present in the top right | Condition holds as described. |
| 5 | Verify the table has three columns: Name (sortable ↕), Value, Actions | Condition holds as described. |
| 6 | Verify each row shows: secret name, masked value in {{secret.name}} format, eye icon, three-dot menu | Condition holds as described. |
| 7 | Verify pagination controls are shown: Rows per page selector, page range label (e.g., "1–10 of 15"), prev/next arrows | Condition holds as described. |

---

## Expected Final State

Verify pagination controls are shown: Rows per page selector, page range label (e.g., "1–10 of 15"), prev/next arrows.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secrets page loads with correct layout and components.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
