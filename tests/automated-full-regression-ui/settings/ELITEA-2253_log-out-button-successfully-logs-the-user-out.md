---
id: ELITEA-2253
title: "Log out button successfully logs the user out"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2253: Log out button successfully logs the user out

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that Log out button successfully logs the user out. Success is confirmed when verify navigating back via browser history does not restore the authenticated session.

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
| 1 | Log in as any user and navigate to Settings | User is authenticated and lands on the expected landing page. |
| 2 | Click "Log out" in the PERSONAL section | Control responds; expected next state is shown. |
| 3 | Verify the user is redirected to the login page | Condition holds as described. |
| 4 | Verify navigating back via browser history does NOT restore the authenticated session | Condition holds as described. |

---

## Expected Final State

Verify navigating back via browser history does NOT restore the authenticated session.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Log out button successfully logs the user out.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
