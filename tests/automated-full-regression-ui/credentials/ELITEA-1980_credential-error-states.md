---
id: ELITEA-1980
title: "Credential — Error States"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_error_states.test_credential_error_states
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1704
---

# ELITEA-1980: Credential — Error States

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the credentials UI displays user-friendly error messages for invalid tokens, unreachable servers, and non-existent credential IDs, without exposing raw stack traces.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Invalid token value | invalid_token_xyz |
| Unreachable Base Url | http://unreachable.example.invalid |
| Non-existent credential URL | /credentials/all/99999 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a credential with an invalid token value (e.g., "invalid_token_xyz") | Credential form accepts the input |
| 2 | Click "Test connection" | Error message appears with a specific failure reason |
| 3 | Attempt to save a credential with a Base Url pointing to an unreachable server | Credential is saved |
| 4 | Click "Test connection" for the unreachable-server credential | Timeout or connection refused error message is displayed |
| 5 | Navigate to a credential details page using an invalid ID in the URL (e.g., /credentials/all/99999) | Appropriate error or not-found state is displayed |
| 6 | Verify all error messages are user-friendly and actionable (not raw stack traces) | Error messages are readable and do not contain stack trace output |

---

## Expected Final State

All error states display clear, user-friendly messages that help the user understand and resolve the issue, without exposing internal error details.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each error scenario displays a user-friendly, actionable message; no raw stack traces are shown.

**Fail:**
- Any step produces an unexpected crash or unhandled error.
- Error messages contain raw stack traces or are not user-friendly.
