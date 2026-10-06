---
id: ELITEA-2246
title: "Viewer and Monitor roles cannot access Secrets section"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2246: Viewer and Monitor roles cannot access Secrets section

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Viewer and Monitor roles cannot access Secrets section. Success is confirmed when verify monitor role is also blocked from accessing secrets.

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
| 1 | Log in as a user with Viewer role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings | Target page/section loads successfully. |
| 3 | Click "Secrets" | Control responds; expected next state is shown. |
| 4 | Verify the section is either not visible in the sidebar OR shows an "Access Denied" / permission error when accessed | Condition holds as described. |
| 5 | Log out and log in as a user with Monitor role | Action completes without error and produces the expected UI state. |
| 6 | Repeat steps 2–4 | Action completes without error and produces the expected UI state. |
| 7 | Verify Monitor role is also blocked from accessing Secrets | Condition holds as described. |

---

## Expected Final State

Verify Monitor role is also blocked from accessing Secrets.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Viewer and Monitor roles cannot access Secrets section.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
