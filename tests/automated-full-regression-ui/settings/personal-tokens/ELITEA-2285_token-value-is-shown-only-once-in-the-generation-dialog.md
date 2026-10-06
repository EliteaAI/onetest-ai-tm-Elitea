---
id: ELITEA-2285
title: "Token value is shown only once in the generation dialog"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2285: Token value is shown only once in the generation dialog

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Token value is shown only once in the generation dialog. Success is confirmed when verify there is no way to retrieve the full token value again except via the eye icon.

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
| 1 | Navigate to Settings → Personal Tokens and click "+" | Target page/section loads successfully. |
| 2 | Enter a name and expiration, click "Generate" | Field accepts the input and displays the entered value. |
| 3 | Verify the full token value is displayed in the "New token generated!" dialog | Condition holds as described. |
| 4 | Verify a "Copy" button is present — click it and verify a success confirmation appears | Condition holds as described. |
| 5 | Close the dialog | Action completes without error and produces the expected UI state. |
| 6 | Verify the Token value column in the table shows a masked "...XXXX" value | Condition holds as described. |
| 7 | Verify there is no way to retrieve the full token value again except via the eye icon | Condition holds as described. |

---

## Expected Final State

Verify there is no way to retrieve the full token value again except via the eye icon.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Token value is shown only once in the generation dialog.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
