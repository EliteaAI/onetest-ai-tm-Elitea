---
id: ELITEA-2244
title: "Navigating away from Settings and back restores the default landing tab"
priority: medium
type: functional
module: settings
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_settings_default_landing_tab_restored.TestSettingsDefaultLandingTabRestored.test_settings_default_landing_tab_restored
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1779"
---

# ELITEA-2244: Navigating away from Settings and back restores the default landing tab

**Module:** settings · **Priority:** medium · **Type:** functional

**Objective:** Verify that Navigating away from Settings and back restores the default landing tab. Success is confirmed when verify the settings page loads without error and content area is not blank.

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
| 2 | Click "Agents" in the left sidebar to navigate away | Control responds; expected next state is shown. |
| 3 | Click "Settings" again | Control responds; expected next state is shown. |
| 4 | Verify the Settings page loads without error and content area is not blank | Condition holds as described. |

---

## Expected Final State

Verify the Settings page loads without error and content area is not blank.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Navigating away from Settings and back restores the default landing tab.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
