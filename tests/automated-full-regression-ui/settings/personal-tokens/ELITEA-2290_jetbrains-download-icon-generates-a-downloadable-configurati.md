---
id: ELITEA-2290
title: "JetBrains download icon generates a downloadable configuration file"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_token_ide_config_download.TestPersonalTokenIdeConfigDownload.test_ide_download_icon_generates_config_file
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1900"
---

# ELITEA-2290: JetBrains download icon generates a downloadable configuration file

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that JetBrains download icon generates a downloadable configuration file. Success is confirmed when verify the downloaded file is not empty and contains valid configuration content.

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
| 2 | Click the JetBrains (red) icon in the Actions column of a token row | Control responds; expected next state is shown. |
| 3 | Verify a file is downloaded | Condition holds as described. |
| 4 | Verify the downloaded file is not empty and contains valid configuration content | Condition holds as described. |

---

## Expected Final State

Verify the downloaded file is not empty and contains valid configuration content.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: JetBrains download icon generates a downloadable configuration file.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
