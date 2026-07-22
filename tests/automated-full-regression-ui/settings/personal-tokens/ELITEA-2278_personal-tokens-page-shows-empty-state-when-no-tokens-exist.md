---
id: ELITEA-2278
title: "Personal Tokens page shows empty state when no tokens exist"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2278: Personal Tokens page shows empty state when no tokens exist

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Personal Tokens page shows empty state when no tokens exist. Success is confirmed when verify the "+" button is still visible and accessible in the empty state.

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
| 1 | Navigate to Settings → Personal Tokens as a user with no tokens created | Target page/section loads successfully. |
| 2 | Verify an empty-state illustration or message is shown (not a blank white area or raw empty table) | Condition holds as described. |
| 3 | Verify the "+" button is still visible and accessible in the empty state | Condition holds as described. |

---

## Expected Final State

Verify the "+" button is still visible and accessible in the empty state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Personal Tokens page shows empty state when no tokens exist.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
