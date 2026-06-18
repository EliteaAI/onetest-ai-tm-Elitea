---
id: ELITEA-1184
title: "Credential ID error message visible across all toolkit types [Parametrized]"
priority: high
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1184: Credential ID error message visible across all toolkit types [Parametrized]

**Module:** Credential Id Visibility · **Priority:** High · **Type:** Functional

**Objective:** Verify that the credential ID/name error message is displayed consistently across different toolkit integrations when the user is missing the required credential.

**Coverage:**
- Error message appears for GitHub, ADO, and Jira toolkit types when credential is missing
- Error contains the credential name/ID in all cases
- Error wording is consistent across toolkit types
- No sensitive credential data is revealed for any toolkit type

## Preconditions

- Logged in to {{base_url}} as User B
- User B has no matching credentials for any of the toolkits listed below
- User A has created toolkits of each type referencing private credentials
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Toolkit types to test: GitHub (credential: `test_github_credential`), ADO (credential: `Ado_cred`), Jira (credential: `jira_cred`)
- User B owns none of the above credentials

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Toolkits. | Toolkits list is displayed. |
| 2 | Open the GitHub toolkit created by User A referencing `test_github_credential`. | Credential field error is shown containing `test_github_credential`. |
| 3 | Open the ADO toolkit created by User A referencing `Ado_cred`. | Credential field error is shown containing `Ado_cred`. |
| 4 | Open the Jira toolkit created by User A referencing `jira_cred`. | Credential field error is shown containing `jira_cred`. |
| 5 | Compare the error message wording across all three toolkits. | Error message format is consistent across all toolkit types. No sensitive data (tokens, secrets) is visible in any error. |
| 6 | Verify the credential field renders (not blank/broken) for all toolkit types. | Credential field is rendered and displays the error state for all three toolkits. |

## Expected Final State

Credential field is rendered and displays the error state for all three toolkits.

## Pass/Fail Criteria

**Pass:**
- Error message with credential name appears for all three toolkit types
- Error wording is consistent across all types
- No sensitive credential data is exposed in any toolkit's error message

**Fail:**
- Error message is missing for one or more toolkit types
- Error does not include the credential name/ID for any toolkit type
- Sensitive credential data appears in any error message
