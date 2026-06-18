---
id: ELITEA-1191
title: "Toolkit with missing credential — error message displays credential name/ID"
priority: high
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1191: Toolkit with missing credential — error message displays credential name/ID

**Module:** Credential Id Visibility · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a toolkit references a private credential the current user does not own, an informative error message is shown that explicitly includes the credential name/ID so the user knows what to create.

**Coverage:**
- Error message is displayed when user does not own the required credential
- Error message contains the exact credential name/ID
- Error includes actionable instructions (e.g., "Please create a credential with the same name")
- No sensitive credential data (token, password, secret) is exposed — only the name/ID

## Preconditions

- Logged in to {{base_url}} as User B
- Project contains a GitHub toolkit created by User A referencing credential `test_github_credential`
- User B has no credential named `test_github_credential`
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Toolkit: GitHub toolkit created by User A
- Missing credential name: `test_github_credential`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Toolkits. | Toolkits list page is displayed. |
| 2 | Open the GitHub toolkit created by User A (e.g., 'test multy' or similar). | Toolkit configuration page opens. |
| 3 | Observe the credential field area (e.g., 'Github configuration'). | An error message is displayed that contains the exact credential name `test_github_credential`. |
| 4 | Read the full error message text. | The error includes actionable instructions such as 'Please create a credential with the same name to use this toolkit'. |
| 5 | Inspect the error message for any sensitive data. | No API tokens, passwords, OAuth secrets, or other sensitive credential payload are visible — only the credential name/ID. |

## Expected Final State

No API tokens, passwords, OAuth secrets, or other sensitive credential payload are visible — only the credential name/ID.

## Pass/Fail Criteria

**Pass:**
- Error message is shown in the credential field area
- Error message contains the credential name `test_github_credential`
- Error includes actionable guidance to create a credential with the same name
- No sensitive credential data is exposed in the error message

**Fail:**
- No error message is shown
- Error message does not include the credential name
- Sensitive credential data is visible in the error message
