---
id: ELITEA-2249
title: "Settings — Secrets page shows empty state when no secrets exist"
priority: medium
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2249: Settings — Secrets page shows empty state when no secrets exist

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Settings — Secrets page shows empty state when no secrets exist. Success is confirmed when verify an "add secret" or "+" button is visible and accessible.

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
| 1 | Navigate to a project with no secrets configured | Target page/section loads successfully. |
| 2 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 3 | Verify an empty-state message or illustration is shown (not a blank area or error) | Condition holds as described. |
| 4 | Verify an "Add Secret" or "+" button is visible and accessible | Condition holds as described. |

---

## Expected Final State

Verify an "Add Secret" or "+" button is visible and accessible.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Settings — Secrets page shows empty state when no secrets exist.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
