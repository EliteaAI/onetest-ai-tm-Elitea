---
id: ELITEA-2245
title: "Admin role has access to all PROJECT settings sections"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2245: Admin role has access to all PROJECT settings sections

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Admin role has access to all PROJECT settings sections. Success is confirmed when verify editable fields are interactive (not read-only).

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
| 1 | Log in as a user with Admin role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings | Target page/section loads successfully. |
| 3 | Click each PROJECT section: AI Configuration, Project Params, Secrets, Users, Analytics | Control responds; expected next state is shown. |
| 4 | Verify each section loads its content without an "Access Denied" or 403 error | Condition holds as described. |
| 5 | Verify editable fields are interactive (not read-only) | Condition holds as described. |

---

## Expected Final State

Verify editable fields are interactive (not read-only).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Admin role has access to all PROJECT settings sections.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
