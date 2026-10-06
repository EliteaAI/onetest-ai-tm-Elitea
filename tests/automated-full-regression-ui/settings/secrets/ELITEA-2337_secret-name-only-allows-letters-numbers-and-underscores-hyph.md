---
id: ELITEA-2337
title: "Secret name only allows letters, numbers, and underscores — hyphens not permitted"
priority: high
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2337: Secret name only allows letters, numbers, and underscores — hyphens not permitted

**Module:** settings-secrets · **Priority:** high · **Type:** functional

**Objective:** Verify that Secret name only allows letters, numbers, and underscores — hyphens not permitted. Success is confirmed when verify no validation error is shown and the checkmark/save icon is enabled.

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
| 1 | Navigate to Settings → Secrets and click "+" | Target page/section loads successfully. |
| 2 | Verify a new inline editable row appears in the table | Condition holds as described. |
| 3 | Enter a name with a hyphen (e.g., "my-secret") | Field accepts the input and displays the entered value. |
| 4 | Verify a validation error is shown or the hyphen is rejected | Condition holds as described. |
| 5 | Enter a name with spaces or special characters (e.g., "my secret!") | Field accepts the input and displays the entered value. |
| 6 | Verify these are also rejected | Condition holds as described. |
| 7 | Enter a valid name "my_secret_123" | Field accepts the input and displays the entered value. |
| 8 | Verify no validation error is shown and the checkmark/save icon is enabled | Condition holds as described. |

---

## Expected Final State

Verify no validation error is shown and the checkmark/save icon is enabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secret name only allows letters, numbers, and underscores — hyphens not permitted.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
