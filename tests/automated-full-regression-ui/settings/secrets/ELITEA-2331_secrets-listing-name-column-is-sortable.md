---
id: ELITEA-2331
title: "Secrets listing — Name column is sortable"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2331: Secrets listing — Name column is sortable

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Secrets listing — Name column is sortable. Success is confirmed when verify the table sorts descending by name.

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
| 1 | Navigate to Settings → Secrets with at least two secrets | Target page/section loads successfully. |
| 2 | Click the Name column header (↕ arrow) | Control responds; expected next state is shown. |
| 3 | Verify the table sorts alphabetically ascending by name | Condition holds as described. |
| 4 | Click the Name column header again | Control responds; expected next state is shown. |
| 5 | Verify the table sorts descending by name | Condition holds as described. |

---

## Expected Final State

Verify the table sorts descending by name.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secrets listing — Name column is sortable.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
