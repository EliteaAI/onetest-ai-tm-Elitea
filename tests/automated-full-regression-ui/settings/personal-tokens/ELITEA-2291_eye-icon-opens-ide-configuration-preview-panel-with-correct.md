---
id: ELITEA-2291
title: "Eye icon opens IDE configuration preview panel with correct content"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_settings_preview.TestPersonalTokenSettingsPreview.test_eye_icon_opens_ide_settings_preview_panel
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1900"
---

# ELITEA-2291: Eye icon opens IDE configuration preview panel with correct content

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Eye icon opens IDE configuration preview panel with correct content. Success is confirmed when close the panel — verify it closes cleanly.

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
| 1 | Navigate to Settings → Personal Tokens with at least one token | Target page/section loads successfully. |
| 2 | Click the eye icon in a token row's Actions column | Control responds; expected next state is shown. |
| 3 | Verify a side panel opens with title "[token name] • VSCode Settings" | Condition holds as described. |
| 4 | Verify a IDE type dropdown is shown (e.g., "VSCode") in the panel header | Condition holds as described. |
| 5 | Verify a copy icon button and a download icon button are present in the panel header | Condition holds as described. |
| 6 | Verify the panel shows a JSON configuration. | Condition holds as described. |
| 7 | Verify no field shows "undefined" or null value unexpectedly | Condition holds as described. |
| 8 | Close the panel — verify it closes cleanly | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Close the panel — verify it closes cleanly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Eye icon opens IDE configuration preview panel with correct content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
