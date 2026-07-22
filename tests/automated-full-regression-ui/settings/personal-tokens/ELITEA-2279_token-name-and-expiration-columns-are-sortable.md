---
id: ELITEA-2279
title: "Token name and expiration columns are sortable"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2279: Token name and expiration columns are sortable

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Token name and expiration columns are sortable. Success is confirmed when verify the table sorts by expiration value.

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
| 1 | Navigate to Settings → Personal Tokens with at least two tokens | Target page/section loads successfully. |
| 2 | Click the Token name column header (↕ arrow) | Control responds; expected next state is shown. |
| 3 | Verify the table sorts tokens alphabetically ascending by name | Condition holds as described. |
| 4 | Click the Token name column header again | Control responds; expected next state is shown. |
| 5 | Verify the table sorts descending by name | Condition holds as described. |
| 6 | Click the Expiration column header | Control responds; expected next state is shown. |
| 7 | Verify the table sorts by expiration value | Condition holds as described. |

---

## Expected Final State

Verify the table sorts by expiration value.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Token name and expiration columns are sortable.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
