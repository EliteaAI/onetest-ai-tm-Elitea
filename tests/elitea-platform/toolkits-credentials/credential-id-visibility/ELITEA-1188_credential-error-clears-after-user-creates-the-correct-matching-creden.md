---
id: ELITEA-1188
title: "Credential error clears after user creates the correct matching credential"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1188: Credential error clears after user creates the correct matching credential

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that once the user creates a credential with the correct name and type, the error in the toolkit configuration is cleared on next page load and the toolkit becomes functional.

**Coverage:**
- Credential error disappears after the user creates a matching credential
- Credential field shows the credential name without error styling after creation
- Toolkit is accessible and functional after the correct credential is created

## Preconditions

- Logged in to {{base_url}} as User B
- The GitHub toolkit currently shows a credential error for `test_github_credential`
- User B does not yet own a credential named `test_github_credential`
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Credential to create: name=`test_github_credential`, type=GitHub
- Toolkit: GitHub toolkit with active credential error

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As User B, navigate to Credentials. Create a new GitHub-type credential named `test_github_credential` with valid GitHub token details. | Credential `test_github_credential` of type GitHub is created and listed under User B's credentials. |
| 2 | Navigate to Toolkits and open the GitHub toolkit that previously showed the credential error. | Toolkit configuration page opens. |
| 3 | Observe the 'Github configuration' credential field. | The credential error is no longer displayed. The field shows `test_github_credential` without error styling. |
| 4 | Open Test Settings and run any available tool. | Tool executes without credential errors. The toolkit is fully functional. |

## Expected Final State

Tool executes without credential errors. The toolkit is fully functional.

## Pass/Fail Criteria

**Pass:**
- Credential error is absent after creating the correct credential
- Credential field displays the name without error styling
- Tool execution succeeds without credential errors

**Fail:**
- Error persists after creating the correct credential (even after page reload)
- Credential field still shows error styling despite a valid matching credential existing
