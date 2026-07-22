---
id: ELITEA-2332
title: "Secrets listing — pagination navigates between pages correctly"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2332: Secrets listing — pagination navigates between pages correctly

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Secrets listing — pagination navigates between pages correctly. Success is confirmed when verify the table updates to show the selected number of rows per page.

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
| 1 | Navigate to Settings → Secrets with more than 10 secrets | Target page/section loads successfully. |
| 2 | Verify the page range shows "1–10 of N" | Condition holds as described. |
| 3 | Click the next page arrow | Control responds; expected next state is shown. |
| 4 | Verify the next set of secrets is shown and page range updates | Condition holds as described. |
| 5 | Change "Rows per page" to a different value | Action completes without error and produces the expected UI state. |
| 6 | Verify the table updates to show the selected number of rows per page | Condition holds as described. |

---

## Expected Final State

Verify the table updates to show the selected number of rows per page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secrets listing — pagination navigates between pages correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
