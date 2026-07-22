---
id: ELITEA-2262
title: "Clicking an index notification link navigates to the correct index"
priority: medium
type: functional
module: settings-notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2262: Clicking an index notification link navigates to the correct index

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking an index notification link navigates to the correct index. Success is confirmed when verify the index page opens without a "not found" error.

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
| 1 | Navigate to Settings → Notifications | Target page/section loads successfully. |
| 2 | Find a notification of type "Index [index link] is successfully created..." | Action completes without error and produces the expected UI state. |
| 3 | Click the index link in the notification text | Control responds; expected next state is shown. |
| 4 | Verify the browser navigates to the referenced index page | Condition holds as described. |
| 5 | Verify the index page opens without a "not found" error | Condition holds as described. |

---

## Expected Final State

Verify the index page opens without a "not found" error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking an index notification link navigates to the correct index.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
