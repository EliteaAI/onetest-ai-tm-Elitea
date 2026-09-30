---
id: ELITEA-3506
title: "Expired/Invalid Token (401) Prompts Re-Authorization"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3506: Expired/Invalid Token (401) Prompts Re-Authorization

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify a 401 from Microsoft Graph during Test Connection is treated as an auth failure requiring re-authorization (`McpAuthorizationRequired`), not a generic error.

## Preconditions

- Credential previously authorized (see ELITEA-3504); its stored access token can be invalidated

## Test Data

- Existing authorized Outlook credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Revoke the app's consent in Azure AD, or otherwise invalidate the stored access/refresh token | Token is now invalid |
| 2 | Click "Test Connection" on the credential | Graph returns 401 |
| 3 | Inspect the raised error | Wrapper raises `McpAuthorizationRequired` with a message containing "invalid or expired" and "re-authorize" |
| 4 | Observe the UI | The UI surfaces this as a fresh authorization prompt (`McpAuthModal`), not as a raw error string |

## Expected Final State

The credential is shown as requiring re-authorization; the authorization modal is available to restart the OAuth flow.

## Pass/Fail Criteria

**Pass:**
- 401 is mapped to `McpAuthorizationRequired` with the documented message content
- UI shows the auth modal, not a raw error

**Fail:**
- 401 surfaces as a generic/raw error
- No re-authorization path is offered
