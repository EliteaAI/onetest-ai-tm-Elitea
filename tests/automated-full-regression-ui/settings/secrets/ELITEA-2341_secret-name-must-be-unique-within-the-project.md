---
id: ELITEA-2341
title: "Secret name must be unique within the project"
priority: high
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2341: Secret name must be unique within the project

**Module:** settings-secrets · **Priority:** high · **Type:** functional

**Objective:** Verify that Secret name must be unique within the project. Success is confirmed when verify no duplicate secret is created.

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
| 1 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 2 | Note the name of any existing secret | Action completes without error and produces the expected UI state. |
| 3 | Click "+" and enter the same name in the new inline row | Control responds; expected next state is shown. |
| 4 | Click the ✓ checkmark to save | Control responds; expected next state is shown. |
| 5 | Verify a validation error is shown (e.g., "Secret with this name already exists") | Condition holds as described. |
| 6 | Verify no duplicate secret is created | Condition holds as described. |

---

## Expected Final State

Verify no duplicate secret is created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secret name must be unique within the project.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
