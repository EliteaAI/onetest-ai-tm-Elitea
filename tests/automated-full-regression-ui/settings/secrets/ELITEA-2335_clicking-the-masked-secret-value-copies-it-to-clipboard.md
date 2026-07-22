---
id: ELITEA-2335
title: "Clicking the masked secret value copies it to clipboard"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2335: Clicking the masked secret value copies it to clipboard

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking the masked secret value copies it to clipboard. Success is confirmed when verify the pasted content is the actual secret value (not the masked reference).

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
| 2 | Locate any secret row showing a masked "{{secret.name}}" value in the Value column | Action completes without error and produces the expected UI state. |
| 3 | Click the masked value text | Control responds; expected next state is shown. |
| 4 | Verify a success confirmation appears (e.g., "Copied!" toast) | Condition holds as described. |
| 5 | Paste the clipboard content into a text editor | Field accepts the input and displays the entered value. |
| 6 | Verify the pasted content is the actual secret value (not the masked reference) | Condition holds as described. |

---

## Expected Final State

Verify the pasted content is the actual secret value (not the masked reference).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking the masked secret value copies it to clipboard.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
