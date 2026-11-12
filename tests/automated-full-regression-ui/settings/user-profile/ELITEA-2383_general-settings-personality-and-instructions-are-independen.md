---
id: ELITEA-2383
title: "DEPRECATED — General settings (personality and instructions) are independent of context management toggle state"
priority: high
type: functional
module: settings-user-profile
status: deprecated
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: [EliteaAI/elitea_issues#6898]
---

# ELITEA-2383: DEPRECATED — General settings independent of context management toggle state

**Deprecation note (2026-11-12):** Step 2 turns the overarching Context Management toggle OFF — that toggle no longer exists per AC4. Since there is no action left to perform, this case's specific verification (General settings unaffected by toggle state) no longer applies. No rewrite target identified; recommend formal deprecation in `index.json`.

Original content retained below for reference only — do not execute.

---

~~**Objective:** Verify that General settings (personality and instructions) are independent of context management toggle state. Success is confirmed when click save — verify the settings save without error.~~

---

## Preconditions (original, no longer applicable)

- User is logged in to the Elitea platform.

---

## Test Data (original, no longer applicable)

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps (original, no longer applicable)

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Personalization | Target page/section loads successfully. |
| 2 | Turn OFF the context management toggle | Action completes without error and produces the expected UI state. |
| 3 | Verify the Default Personality dropdown and Default User Instructions textarea remain editable and are NOT grayed out | Condition holds as described. |
| 4 | Change the Default Personality to "Quirky" | Action completes without error and produces the expected UI state. |
| 5 | Click Save — verify the settings save without error | Control responds; expected next state is shown. |

---

## Expected Final State (original, no longer applicable)

Click Save — verify the settings save without error.

---

## Pass/Fail Criteria (original, no longer applicable)

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: General settings (personality and instructions) are independent of context management toggle state.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
