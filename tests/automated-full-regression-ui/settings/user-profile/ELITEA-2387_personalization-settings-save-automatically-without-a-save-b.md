---
id: ELITEA-2387
title: "Personalization settings save automatically without a Save button"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2387: Personalization settings save automatically without a Save button

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Personalization settings save automatically without a Save button. Success is confirmed when verify default personality still shows "qa" (auto-saved without explicit save action).

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
| 1 | Navigate to Settings → Personalization | Target page/section loads successfully. |
| 2 | Verify there is no "Save" button on the page | Condition holds as described. |
| 3 | Change Default Personality to "QA" | Action completes without error and produces the expected UI state. |
| 4 | Navigate away to any other page (e.g., Settings → Notifications) | Target page/section loads successfully. |
| 5 | Navigate back to Settings → Personalization | Target page/section loads successfully. |
| 6 | Verify Default Personality still shows "QA" (auto-saved without explicit save action) | Condition holds as described. |

---

## Expected Final State

Verify Default Personality still shows "QA" (auto-saved without explicit save action).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Personalization settings save automatically without a Save button.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
