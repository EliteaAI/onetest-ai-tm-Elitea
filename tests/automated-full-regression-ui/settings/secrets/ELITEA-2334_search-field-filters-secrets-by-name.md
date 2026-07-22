---
id: ELITEA-2334
title: "Search field filters secrets by name"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2334: Search field filters secrets by name

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Search field filters secrets by name. Success is confirmed when clear the search field — verify all secrets are shown again.

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
| 1 | Navigate to Settings → Secrets with at least two secrets with different names | Target page/section loads successfully. |
| 2 | Type a partial name in the Search field | Field accepts the input and displays the entered value. |
| 3 | Verify the table filters to show only matching secret names | Condition holds as described. |
| 4 | Verify the search is case-insensitive | Condition holds as described. |
| 5 | Clear the search field — verify all secrets are shown again | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Clear the search field — verify all secrets are shown again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Search field filters secrets by name.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
