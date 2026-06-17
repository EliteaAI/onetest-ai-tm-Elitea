---
id: ELITEA-1193
title: "Toolkit with matching credential — no error shown and configuration loads normally"
priority: high
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1193: Toolkit with matching credential — no error shown and configuration loads normally

**Module:** Credential Id Visibility · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the current user owns a credential whose name matches the one referenced in the toolkit, no error is shown and the toolkit configuration is accessible normally.

**Coverage:**
- Credential field shows the credential name without any error banner or warning
- Toolkit configuration panel loads fully without validation errors
- Toolkit save/test operation completes without credential-related errors

## Preconditions

- Logged in to {{base_url}} as User B
- User B owns a GitHub-type credential named `test_github_credential`
- Project contains a GitHub toolkit referencing `test_github_credential`
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Credential name: `test_github_credential`
- Credential type: GitHub

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Credentials and verify a GitHub-type credential named `test_github_credential` exists. | Credential `test_github_credential` of type GitHub is listed. |
| 2 | Navigate to Toolkits. Open the GitHub toolkit referencing `test_github_credential`. | Toolkit configuration page opens. |
| 3 | Observe the 'Github configuration' credential field. | Credential field shows `test_github_credential` with no error banner, warning icon, or red styling. |
| 4 | Verify the full toolkit configuration panel has loaded. | All configuration fields are visible and editable. No validation errors are shown. |
| 5 | Open Test Settings and run any available tool. | Tool executes without credential-related errors. |

## Expected Final State

Tool executes without credential-related errors.

## Pass/Fail Criteria

**Pass:**
- Credential field displays `test_github_credential` without any error or warning
- Toolkit configuration loads fully
- No credential errors appear on save or tool execution

**Fail:**
- Error message appears despite user owning the correct credential
- Toolkit configuration fails to load
- Tool execution shows a credential error
