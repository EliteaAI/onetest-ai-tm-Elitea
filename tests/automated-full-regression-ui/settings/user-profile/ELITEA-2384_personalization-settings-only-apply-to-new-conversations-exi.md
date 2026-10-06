---
id: ELITEA-2384
title: "Personalization settings only apply to new conversations — existing conversations are unaffected"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2384: Personalization settings only apply to new conversations — existing conversations are unaffected

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Personalization settings only apply to new conversations — existing conversations are unaffected. Success is confirmed when verify the new conversation uses the updated personality setting.

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
| 1 | Open an existing chat conversation and note its current behavior/settings | Target page/section loads successfully. |
| 2 | Navigate to Personalization and change Default Personality to a different option | Target page/section loads successfully. |
| 3 | Return to the existing conversation | Action completes without error and produces the expected UI state. |
| 4 | Verify the existing conversation settings have NOT changed | Condition holds as described. |
| 5 | Create a new conversation | Operation completes successfully; state updates and confirmation is shown. |
| 6 | Verify the new conversation uses the updated personality setting | Condition holds as described. |

---

## Expected Final State

Verify the new conversation uses the updated personality setting.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Personalization settings only apply to new conversations — existing conversations are unaffected.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
