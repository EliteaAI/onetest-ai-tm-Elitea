---
id: ELITEA-2400
title: "Edit an existing Vector Storage configuration"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_vector_storage_edit.TestEditVectorStorageConfiguration.test_edit_pgvector_display_name
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1990"
---

# ELITEA-2400: Edit an existing Vector Storage configuration

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Edit an existing Vector Storage configuration. Success is confirmed when verify the card reflects the updated display name.

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
| 1 | Navigate to Settings → AI Configuration → Vector Storage section | Target page/section loads successfully. |
| 2 | Click on an existing vector storage card | Control responds; expected next state is shown. |
| 3 | Verify the edit form opens with pre-populated values | Condition holds as described. |
| 4 | Update the Display Name to "Autotest PGVector Edited" | Action completes without error and produces the expected UI state. |
| 5 | Click Save | Control responds; expected next state is shown. |
| 6 | Verify the card reflects the updated Display Name | Condition holds as described. |

---

## Expected Final State

Verify the card reflects the updated Display Name.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Edit an existing Vector Storage configuration.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
