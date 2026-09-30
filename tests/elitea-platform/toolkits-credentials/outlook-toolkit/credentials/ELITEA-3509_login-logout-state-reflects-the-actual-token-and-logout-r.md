---
id: ELITEA-3509
title: "Login/Logout State Reflects the Actual Token, and Logout Revokes Local Session Correctly"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3509: Login/Logout State Reflects the Actual Token, and Logout Revokes Local Session Correctly

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify the Login/Logout button on the credential form accurately reflects `isOAuthLoggedIn` and that Logout clears only this credential's token.

## Preconditions

- An Outlook credential authorized per ELITEA-3504

## Test Data

- Existing authorized Outlook credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the authorized Outlook credential | Button shows "Logout" (not "Login") |
| 2 | Click "Logout" | `McpLogoutModal` confirmation dialog appears |
| 3 | Confirm the logout | Toast "You have successfully logged out!" appears; button reverts to "Login" |
| 4 | Click "Test Connection" again | Re-authorization is required; no stale token is reused |

## Expected Final State

The credential is logged out; a fresh OAuth flow is required to reconnect.

## Pass/Fail Criteria

**Pass:**
- Button state accurately reflects token presence at every step
- Logout confirmation and success toast appear
- Post-logout Test Connection requires re-authorization

**Fail:**
- Button shows "Logout" without a valid token, or vice versa
- Logout silently fails or leaves a reusable token
