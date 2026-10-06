---
id: ELITEA-2283
title: "Token can be created without an expiration date"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2283: Token can be created without an expiration date

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Token can be created without an expiration date. Success is confirmed when verify the expiration column shows "never" or equivalent (not a blank cell or error).

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
| 2 | Enter a token name and select "Never" | Field accepts the input and displays the entered value. |
| 3 | Click "Generate" and close the success dialog | Control responds; expected next state is shown. |
| 4 | Verify the token appears in the table | Condition holds as described. |
| 5 | Verify the Expiration column shows "Never" or equivalent (not a blank cell or error) | Condition holds as described. |

---

## Expected Final State

Verify the Expiration column shows "Never" or equivalent (not a blank cell or error).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Token can be created without an expiration date.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
