---
id: ELITEA-2250
title: "Settings — Personal Tokens page shows empty state when no tokens exist"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2250: Settings — Personal Tokens page shows empty state when no tokens exist

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Settings — Personal Tokens page shows empty state when no tokens exist. Success is confirmed when verify a "create token" or "+" button is visible and accessible.

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
| 2 | Verify an empty-state message or illustration is shown | Condition holds as described. |
| 3 | Verify a "Create token" or "+" button is visible and accessible | Condition holds as described. |

---

## Expected Final State

Verify a "Create token" or "+" button is visible and accessible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Settings — Personal Tokens page shows empty state when no tokens exist.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
