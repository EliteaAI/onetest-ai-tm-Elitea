---
id: ELITEA-1971
title: "Credential — Discard Changes"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
automation_test_id: tests.ui.toolkits.test_credential_discard_changes.TestCredentialDiscardChanges.test_credential_discard_changes_reverts_display_name
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/519
---

# ELITEA-1971: Credential — Discard Changes

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Discard button reverts unsaved changes to a credential's fields after showing a confirmation modal, and that the Save button returns to a disabled state after discarding.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Initial Display Name | autotest_discard_cred |
| Changed Display Name | autotest_changed |
| Credential type | Github |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a credential "autotest_discard_cred" of type Github | Credential is created successfully |
| 2 | Open the credential details page for "autotest_discard_cred" | Credential detail page loads with the original Display Name |
| 3 | Change Display Name to "autotest_changed" | Input field shows "autotest_changed" |
| 4 | Verify the Discard button becomes enabled | Discard button is active/clickable |
| 5 | Click Discard | Warning modal opens with message "Are you sure you want to discard changes?" |
| 6 | Verify the confirmation modal is displayed with the expected message | Modal is visible with "Are you sure you want to discard changes?" |
| 7 | Click the "Discard" button in the modal | Modal closes and changes are reverted |
| 8 | Verify Display Name reverts to "autotest_discard_cred" | Field shows the original name |
| 9 | Verify the Save button returns to disabled state | Save button is inactive/not clickable |

---

## Expected Final State

After discarding, the credential's Display Name is reverted to "autotest_discard_cred" and the Save button is disabled, indicating no pending changes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Display Name reverts to original value after discarding; Save button returns to disabled state.

**Fail:**
- Any step produces an error or unexpected result.
- Changes are not reverted, the confirmation modal does not appear, or the Save button remains enabled after discard.
