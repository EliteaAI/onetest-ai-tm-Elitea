---
id: ELITEA-2294
title: "Users page search filters the table in real time"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2294: Users page search filters the table in real time

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Users page search filters the table in real time. Success is confirmed when clear search — verify all users are shown again.

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
| 1 | Navigate to Settings → Users as Admin | Target page/section loads successfully. |
| 2 | Type a partial email in the Search field | Field accepts the input and displays the entered value. |
| 3 | Verify the table filters to show only matching users | Condition holds as described. |
| 4 | Clear search and type a partial name | Action completes without error and produces the expected UI state. |
| 5 | Verify the table filters to show only matching names | Condition holds as described. |
| 6 | Clear search — verify all users are shown again | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Clear search — verify all users are shown again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Users page search filters the table in real time.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
