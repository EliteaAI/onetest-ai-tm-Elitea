---
id: ELITEA-2375
title: "DEPRECATED — Disabling context management also deactivates summarization regardless of summarization toggle state"
priority: medium
type: functional
module: settings-user-profile
status: deprecated
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: [EliteaAI/elitea_issues#6898]
---

# ELITEA-2375: DEPRECATED — Disabling context management also deactivates summarization regardless of summarization toggle state

**Deprecation note (2026-11-12):** This case's entire premise depends on turning the overarching Context Management toggle OFF to verify Summarization becomes inactive. That toggle was removed per EliteaAI/elitea_issues#6898 AC4 ("togle was deleted") — there is no longer an action to perform. No rewrite target identified; recommend formal deprecation in `index.json`.

Original content retained below for reference only — do not execute.

---

~~**Objective:** Verify that Disabling context management also deactivates summarization regardless of summarization toggle state. Success is confirmed when verify summarization settings become active again.~~

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
| 1 | Navigate to  Personalization | Target page/section loads successfully. |
| 2 | Enable both context management and summarization toggles | Action completes without error and produces the expected UI state. |
| 3 | Turn context management toggle OFF | Action completes without error and produces the expected UI state. |
| 4 | Verify the summarization toggle appears grayed out / inactive | Condition holds as described. |
| 5 | Verify the summarization fields (Summarization Instructions, Target Summary Tokens) are uneditable | Condition holds as described. |
| 6 | Turn context management back ON | Action completes without error and produces the expected UI state. |
| 7 | Verify summarization settings become active again | Condition holds as described. |

---

## Expected Final State (original, no longer applicable)

Verify summarization settings become active again.

---

## Pass/Fail Criteria (original, no longer applicable)

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Disabling context management also deactivates summarization regardless of summarization toggle state.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
