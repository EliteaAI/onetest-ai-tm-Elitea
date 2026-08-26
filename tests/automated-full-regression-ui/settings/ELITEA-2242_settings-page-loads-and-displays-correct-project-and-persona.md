---
id: ELITEA-2242
title: "Settings page loads and displays correct PROJECT and PERSONAL sections"
priority: high
type: functional
module: settings
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_settings_page_sections_and_default_tab.TestSettingsPageSectionsAndDefaultTab.test_settings_page_sections_and_default_tab
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1779"
---

# ELITEA-2242: Settings page loads and displays correct PROJECT and PERSONAL sections

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that Settings page loads and displays correct PROJECT and PERSONAL sections. Success is confirmed when verify the main content area loads the ai configuration page without blank or error state.

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
| 1 | Log in as a user with admin role | User is authenticated and lands on the expected landing page. |
| 2 | Click "Settings" in the left sidebar | Control responds; expected next state is shown. |
| 3 | Verify the Settings page loads without error | Condition holds as described. |
| 4 | Verify the left panel shows two groups: | Condition holds as described. |
| 5 | PROJECT: AI Configuration, Project Params, Secrets, Users, Analytics | Action completes without error and produces the expected UI state. |
| 6 | PERSONAL: Personalization, Personal Tokens, Notifications, Log out | Action completes without error and produces the expected UI state. |
| 7 | Verify "AI Configuration" is selected and active by default | Condition holds as described. |
| 8 | Verify the main content area loads the AI Configuration page without blank or error state | Condition holds as described. |

---

## Expected Final State

Verify the main content area loads the AI Configuration page without blank or error state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Settings page loads and displays correct PROJECT and PERSONAL sections.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
