---
id: ELITEA-2342
title: "Value column shows {{secret.name}} reference format when secret is masked"
priority: high
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2342: Value column shows {{secret.name}} reference format when secret is masked

**Module:** settings-secrets · **Priority:** high · **Type:** functional

**Objective:** Verify that Value column shows {{secret.name}} reference format when secret is masked. Success is confirmed when verify the format exactly matches the secret's name (e.g., secret named "auth_token" shows "{{secret.auth_token}}").

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
| 2 | Verify each secret row in the Value column shows the reference format "{{secret.<name>}}" | Condition holds as described. |
| 3 | Verify the format exactly matches the secret's name (e.g., secret named "auth_token" shows "{{secret.auth_token}}") | Condition holds as described. |

---

## Expected Final State

Verify the format exactly matches the secret's name (e.g., secret named "auth_token" shows "{{secret.auth_token}}").

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Value column shows {{secret.name}} reference format when secret is masked.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
