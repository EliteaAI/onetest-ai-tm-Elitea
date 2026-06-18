---
id: ELITEA-1189
title: "Toolkit credential type mismatch — error shown, wrong-type credential not applied"
priority: high
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1189: Toolkit credential type mismatch — error shown, wrong-type credential not applied

**Module:** Credential Id Visibility · **Priority:** High · **Type:** Functional

**Objective:** Verify that if the user has a credential with the same name as the toolkit's required credential but of a different type, the toolkit shows an error and does NOT silently apply the mismatched credential.

**Coverage:**
- Error is shown when credential name matches but type is wrong
- Error message makes clear the credential is unavailable or type does not match
- Wrong-type credential is NOT silently applied to the toolkit
- Tool execution fails with a credential error, not a runtime/API crash from using wrong credential data

## Preconditions

- Logged in to {{base_url}} as User B
- User B owns a Jira-type credential named `test_github_credential` (same name, wrong type)
- Project contains a GitHub toolkit requiring a GitHub-type credential named `test_github_credential`
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Credential name: `test_github_credential`
- User B credential type: Jira (wrong)
- Required credential type: GitHub

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B. Navigate to Credentials. Confirm a Jira-type credential named `test_github_credential` exists. | A Jira-type credential named `test_github_credential` is listed under User B's credentials. |
| 2 | Navigate to Toolkits. Open the GitHub toolkit that requires a GitHub credential named `test_github_credential`. | Toolkit configuration page opens. |
| 3 | Observe the 'Github configuration' credential field. | An error is shown indicating the credential is unavailable or the type does not match. No successful credential match is displayed. |
| 4 | Verify the Jira credential has not been silently applied — inspect the credential field value. | The credential field does not show a successful match. The Jira credential is not accepted as valid for the GitHub toolkit. |
| 5 | Open Test Settings. Attempt to run any tool. | Tool execution fails with a credential-related error. There is no unexpected API/runtime error caused by wrong credential data being used silently. |

## Expected Final State

Tool execution fails with a credential-related error. There is no unexpected API/runtime error caused by wrong credential data being used silently.

## Pass/Fail Criteria

**Pass:**
- Error is displayed for the credential field when type mismatches
- Jira credential is NOT accepted or applied to the GitHub toolkit
- Tool execution produces a credential error, not a silent wrong-credential API failure

**Fail:**
- Jira credential is silently accepted as a GitHub credential
- No error is shown despite type mismatch
- Tool executes using wrong credential data (even if it then fails at the API level)
