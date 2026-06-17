---
id: ELITEA-1186
title: "Credential error message exposes only name/ID — no sensitive data leaked"
priority: medium
type: functional
module: credential-id-visibility
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2692, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#2692]
---
# ELITEA-1186: Credential error message exposes only name/ID — no sensitive data leaked

**Module:** Credential Id Visibility · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the toolkit credential error message shows only the credential name/ID and actionable guidance, and never leaks token values, passwords, or secrets — both in the UI and in API responses.

**Coverage:**
- Error message text contains only credential name and actionable guidance
- No API token, OAuth secret, or password visible in the UI error
- Network API responses do not return sensitive credential payload to User B

## Preconditions

- Logged in to {{base_url}} as User B
- The GitHub toolkit with missing `test_github_credential` is accessible to User B
- Browser DevTools available
- Browser: Chrome

## Test Data

- ELITEA URL: {{base_url}}
- Missing credential: `test_github_credential`
- Sensitive data to check for: API token, OAuth client secret, password fields in API responses

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open browser DevTools (F12). Navigate to the Network tab. | Network tab is open and recording. |
| 2 | Navigate to the GitHub toolkit with the credential error. Observe the error message text in the UI. | Error message contains the credential name `test_github_credential` and actionable instructions. No API token, OAuth secret, or password values are visible in the UI error text. |
| 3 | In the Network tab, filter for API requests triggered during the toolkit page load. Inspect response bodies for any credentials-related endpoints. | API responses do not contain sensitive credential payload (token values, secrets, passwords) for User B. Only the credential name/ID and status are returned. |
| 4 | Verify the error wording: it should contain the credential name shown as `test_github_credential` and guidance like 'Please create a credential with the same name'. | Error message matches expected pattern. No sensitive data is present anywhere in the page source or network responses. |

## Expected Final State

Error message matches expected pattern. No sensitive data is present anywhere in the page source or network responses.

## Pass/Fail Criteria

**Pass:**
- UI error message contains only credential name/ID and actionable guidance
- No sensitive credential data visible in UI or browser DevTools network responses

**Fail:**
- Token, secret, or password values appear in the UI error message
- API response returned to User B contains sensitive credential payload
