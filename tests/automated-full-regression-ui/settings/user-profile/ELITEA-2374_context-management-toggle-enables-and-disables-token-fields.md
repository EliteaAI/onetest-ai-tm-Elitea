---
id: ELITEA-2374
title: "Context management toggle enables and disables token fields"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2374: Context management toggle enables and disables token fields

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Context management toggle enables and disables token fields. Success is confirmed when click the toggle back on — verify both fields and summarization become editable again.

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
| 1 | Navigate to Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Verify the "Enable context management for new conversations" toggle is present | Condition holds as described. |
| 3 | Verify when toggle is ON: Max Context Tokens and Preserve Recent Messages fields are editable | Condition holds as described. |
| 4 | Verify default values: Max Context Tokens = 64000, Preserve Recent Messages = 5 | Condition holds as described. |
| 5 | Click the toggle to turn it OFF | Control responds; expected next state is shown. |
| 6 | Verify Max Context Tokens and Preserve Recent Messages become grayed out and uneditable | Condition holds as described. |
| 7 | Verify the DEFAULT SUMMARIZATION sub-section also becomes inactive (toggle grayed out or disabled) | Condition holds as described. |
| 8 | Click the toggle back ON — verify both fields and summarization become editable again | Control responds; expected next state is shown. |

---

## Expected Final State

Click the toggle back ON — verify both fields and summarization become editable again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Context management toggle enables and disables token fields.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
