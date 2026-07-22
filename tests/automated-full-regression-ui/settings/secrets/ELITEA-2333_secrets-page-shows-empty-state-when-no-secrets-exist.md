---
id: ELITEA-2333
title: "Secrets page shows empty state when no secrets exist"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2333: Secrets page shows empty state when no secrets exist

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Secrets page shows empty state when no secrets exist. Success is confirmed when verify the "+" button is still visible and accessible.

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
| 1 | Navigate to Settings → Secrets in a project with no secrets | Target page/section loads successfully. |
| 2 | Verify an empty-state message or illustration is shown (not a blank area or error) | Condition holds as described. |
| 3 | Verify the "+" button is still visible and accessible | Condition holds as described. |

---

## Expected Final State

Verify the "+" button is still visible and accessible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secrets page shows empty state when no secrets exist.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
