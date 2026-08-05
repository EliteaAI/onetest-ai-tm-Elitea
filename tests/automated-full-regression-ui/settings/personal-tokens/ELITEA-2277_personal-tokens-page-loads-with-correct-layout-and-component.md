---
id: ELITEA-2277
title: "Personal Tokens page loads with correct layout and components"
priority: medium
type: functional
module: settings-personal-tokens
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_personal_tokens_page_layout.TestPersonalTokensPageLayout.test_personal_tokens_page_layout_and_components
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1172
---

# ELITEA-2277: Personal Tokens page loads with correct layout and components

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Personal Tokens page loads with correct layout and components. Success is confirmed when verify each token row in actions column shows exactly four icons: eye, vscode, jetbrains, trash.

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
| 1 | Navigate to Settings → Personal Tokens | Target page/section loads successfully. |
| 2 | Verify the page header shows "Personal Tokens" | Condition holds as described. |
| 3 | Verify a "Search tokens..." input is present in the top right | Condition holds as described. |
| 4 | Verify a "+" button is present in the top right | Condition holds as described. |
| 5 | Verify the tokens table has exactly four columns: Token name, Token value, Expiration, Actions | Condition holds as described. |
| 6 | Verify each token row in Actions column shows exactly four icons: eye, VSCode, JetBrains, trash | Condition holds as described. |

---

## Expected Final State

Verify each token row in Actions column shows exactly four icons: eye, VSCode, JetBrains, trash.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Personal Tokens page loads with correct layout and components.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
