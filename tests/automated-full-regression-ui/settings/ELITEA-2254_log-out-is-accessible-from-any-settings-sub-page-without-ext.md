---
id: ELITEA-2254
title: "Log out is accessible from any Settings sub-page without extra navigation"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2254: Log out is accessible from any Settings sub-page without extra navigation

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that Log out is accessible from any Settings sub-page without extra navigation. Success is confirmed when click "log out" and verify the user is redirected to the login page.

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
| 1 | Log in and navigate to Settings → Personal Tokens | User is authenticated and lands on the expected landing page. |
| 2 | Without clicking any other sidebar item, verify "Log out" is visible in the sidebar | Action completes without error and produces the expected UI state. |
| 3 | Click "Log out" and verify the user is redirected to the login page | Control responds; expected next state is shown. |

---

## Expected Final State

Click "Log out" and verify the user is redirected to the login page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Log out is accessible from any Settings sub-page without extra navigation.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
