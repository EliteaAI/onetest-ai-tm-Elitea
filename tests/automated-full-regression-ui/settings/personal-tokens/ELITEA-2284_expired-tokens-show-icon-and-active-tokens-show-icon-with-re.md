---
id: ELITEA-2284
title: "Expired tokens show ⊗ icon and active tokens show ✅ icon with remaining days"
priority: high
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2284: Expired tokens show ⊗ icon and active tokens show ✅ icon with remaining days

**Module:** settings-personal-tokens · **Priority:** high · **Type:** functional

**Objective:** Verify that Expired tokens show ⊗ icon and active tokens show ✅ icon with remaining days. Success is confirmed when verify the expiration column shows a green ✅ icon and "in x days" label.

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
| 1 | Navigate to Settings → Personal Tokens | Target page/section loads successfully. |
| 2 | Locate a token whose expiration date has passed | Action completes without error and produces the expected UI state. |
| 3 | Verify the Expiration column shows an ⊗ icon and "Expired" label | Condition holds as described. |
| 4 | Locate a token that is still active | Action completes without error and produces the expected UI state. |
| 5 | Verify the Expiration column shows a green ✅ icon and "in X days" label | Condition holds as described. |

---

## Expected Final State

Verify the Expiration column shows a green ✅ icon and "in X days" label.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Expired tokens show ⊗ icon and active tokens show ✅ icon with remaining days.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
