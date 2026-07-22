---
id: ELITEA-2248
title: "Unauthenticated user is redirected to login when accessing Settings directly"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2248: Unauthenticated user is redirected to login when accessing Settings directly

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that Unauthenticated user is redirected to login when accessing Settings directly. Success is confirmed when verify no settings content is visible to the unauthenticated user.

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
| 1 | Log out of the platform | Action completes without error and produces the expected UI state. |
| 2 | Attempt to navigate directly to the Settings URL | Action completes without error and produces the expected UI state. |
| 3 | Verify the user is redirected to the login page | Condition holds as described. |
| 4 | Verify no Settings content is visible to the unauthenticated user | Condition holds as described. |

---

## Expected Final State

Verify no Settings content is visible to the unauthenticated user.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Unauthenticated user is redirected to login when accessing Settings directly.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
