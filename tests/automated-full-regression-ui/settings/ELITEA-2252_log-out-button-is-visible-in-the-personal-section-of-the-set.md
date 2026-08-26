---
id: ELITEA-2252
title: "Log out button is visible in the PERSONAL section of the Settings sidebar"
priority: medium
type: functional
module: settings
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_settings_profile_logout_button_visible.TestSettingsProfileLogoutButtonVisible.test_settings_profile_logout_button_visible
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1779"
---

# ELITEA-2252: Log out button is visible in the PERSONAL section of the Settings sidebar

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Log out button is visible in the PERSONAL section of the Settings sidebar. Success is confirmed when verify it is visible without any additional scrolling or expanding.

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
| 1 | Log in as any user role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings | Target page/section loads successfully. |
| 3 | Verify "Log out" is visible as the last item in the PERSONAL section | Condition holds as described. |
| 4 | Verify it has a recognizable log out icon | Condition holds as described. |
| 5 | Verify it is visible without any additional scrolling or expanding | Condition holds as described. |

---

## Expected Final State

Verify it is visible without any additional scrolling or expanding.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Log out button is visible in the PERSONAL section of the Settings sidebar.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
