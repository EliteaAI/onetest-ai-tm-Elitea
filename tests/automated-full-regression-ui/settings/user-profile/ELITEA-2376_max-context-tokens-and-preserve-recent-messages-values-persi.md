---
id: ELITEA-2376
title: "Context Window Mode and Preserve Recent Messages Values Persist After Save and Reload"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings, feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6898]
---

# ELITEA-2376: Context Window Mode and Preserve Recent Messages Values Persist After Save and Reload

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Rewrite note (2026-11-12):** Original case set a numeric "Max Context Tokens=32000" value, which no longer exists per EliteaAI/elitea_issues#6898. Rewritten to use the new Context window radio (Balanced/Full); "Preserve Recent Messages" is unaffected and kept as-is.

**Objective:** Verify that the Context window mode (Balanced/Full) and Preserve Recent Messages values persist after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.

---

## Test Data

| Field | Value |
|-------|-------|
| Context window mode | Full |
| Preserve Recent Messages | 10 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Select "Full" in the Context window radio group | Action completes without error and produces the expected UI state. |
| 3 | Set Preserve Recent Messages to 10 | Action completes without error and produces the expected UI state. |
| 4 | Click somewhere on UI to trigger autosave | Control responds; expected next state is shown. |
| 5 | Reload the page | Action completes without error and produces the expected UI state. |
| 6 | Verify Context window shows "Full" and Preserve Recent Messages shows 10 | Condition holds as described. |

---

## Expected Final State

Context window shows "Full" and Preserve Recent Messages shows 10 after reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both values persist correctly after reload.

**Fail:**
- Any step produces an error or unexpected result.
- Either value reverts or fails to save.
