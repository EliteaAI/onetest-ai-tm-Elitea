---
id: ELITEA-2415
title: "Test connection button shows error for invalid or expired credentials"
priority: high
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_ai_credential_test_connection.test_ai_credential_test_connection_error_then_success
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1995"
---

# ELITEA-2415: Test connection button shows error for invalid or expired credentials

**Module:** settings-ai-configuration · **Priority:** high · **Type:** functional

**Objective:** Verify that Test connection button shows error for invalid or expired credentials. Success is confirmed when verify the connection test now succeeds with a success indicator.

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
| 1 | Navigate to Settings → Credentials | Target page/section loads successfully. |
| 2 | Click "+" to create a new credential | Control responds; expected next state is shown. |
| 3 | Fill in the credential fields with invalid or expired values (e.g., a known bad API key) | Field accepts the input and displays the entered value. |
| 4 | Click the "Test Connection" button | Control responds; expected next state is shown. |
| 5 | Verify a user-friendly error message is shown (e.g., "Connection failed" or "Invalid API key") | Condition holds as described. |
| 6 | Verify the form remains open for correction (user is not redirected away) | Condition holds as described. |
| 7 | Correct the credential values and click "Test Connection" again | Action completes without error and produces the expected UI state. |
| 8 | Verify the connection test now succeeds with a success indicator | Condition holds as described. |

---

## Expected Final State

Verify the connection test now succeeds with a success indicator.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Test connection button shows error for invalid or expired credentials.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
