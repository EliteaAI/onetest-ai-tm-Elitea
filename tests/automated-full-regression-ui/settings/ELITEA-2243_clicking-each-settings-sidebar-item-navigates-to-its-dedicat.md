---
id: ELITEA-2243
title: "Clicking each Settings sidebar item navigates to its dedicated page"
priority: medium
type: functional
module: settings
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_settings_sidebar_item_navigation.TestSettingsSidebarItemNavigation.test_settings_sidebar_item_navigation
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1779"
---

# ELITEA-2243: Clicking each Settings sidebar item navigates to its dedicated page

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking each Settings sidebar item navigates to its dedicated page. Success is confirmed when verify "log out" is visible as the last personal item and does not navigate to a settings sub-page.

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
| 1 | Navigate to Settings | Target page/section loads successfully. |
| 2 | Click each PROJECT section item one by one: AI Configuration, Project Params, Secrets, Users, Analytics | Control responds; expected next state is shown. |
| 3 | For each click verify the content area updates to that section's page (not blank, not the previous section) | Action completes without error and produces the expected UI state. |
| 4 | Click each PERSONAL section item one by one: Personalization, Personal Tokens, Notifications | Control responds; expected next state is shown. |
| 5 | For each click verify the content area updates to that section's page | Action completes without error and produces the expected UI state. |
| 6 | Verify "Log out" is visible as the last PERSONAL item and does NOT navigate to a settings sub-page | Condition holds as described. |

---

## Expected Final State

Verify "Log out" is visible as the last PERSONAL item and does NOT navigate to a settings sub-page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking each Settings sidebar item navigates to its dedicated page.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
