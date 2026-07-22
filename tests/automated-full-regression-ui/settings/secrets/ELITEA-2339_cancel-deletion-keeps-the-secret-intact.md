---
id: ELITEA-2339
title: "Cancel deletion keeps the secret intact"
priority: high
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2339: Cancel deletion keeps the secret intact

**Module:** settings-secrets · **Priority:** high · **Type:** functional

**Objective:** Verify that Cancel deletion keeps the secret intact. Success is confirmed when verify the secret remains in the table unchanged.

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
| 2 | Click the three-dot menu → Delete on any secret | Control responds; expected next state is shown. |
| 3 | Verify a confirmation dialog appears | Condition holds as described. |
| 4 | Click Cancel | Control responds; expected next state is shown. |
| 5 | Verify the secret remains in the table unchanged | Condition holds as described. |

---

## Expected Final State

Verify the secret remains in the table unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Cancel deletion keeps the secret intact.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
