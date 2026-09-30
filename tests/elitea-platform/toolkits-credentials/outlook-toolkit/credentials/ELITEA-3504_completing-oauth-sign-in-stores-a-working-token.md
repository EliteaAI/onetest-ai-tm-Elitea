---
id: ELITEA-3504
title: "Completing OAuth Sign-In Stores a Working Token"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3504: Completing OAuth Sign-In Stores a Working Token

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify completing the Microsoft consent screen in the popup results in a successful, persisted authorization that survives a page reload.

## Preconditions

- ELITEA-3503 completed up to the point of an open `McpAuthModal` with an "Authorize" button
- A valid Microsoft 365 test account able to complete sign-in/consent

## Test Data

- Live Microsoft 365 test mailbox credentials

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click "Authorize" and complete Microsoft sign-in/consent in the popup | Popup completes without error |
| 2 | Observe the modal | Modal shows "✓ Authorization successful! ..." and auto-closes |
| 3 | Click "Test Connection" again | Connection succeeds (Graph `GET /me/mailFolders?$top=1` returns 200); no error shown in the `credential-form-api-error-message` area |
| 4 | Reload the Credentials page and reopen this credential | Credential shows as logged in (Logout button visible instead of Login) |

## Expected Final State

The credential is authorized, its token is stored, and it remains logged in after a page reload.

## Pass/Fail Criteria

**Pass:**
- Modal shows success message and auto-closes
- Test Connection succeeds after authorization
- Logged-in state persists across a reload

**Fail:**
- Success message does not appear, or modal does not auto-close
- Test Connection fails after a completed OAuth flow
- Credential reverts to "Login" state after reload despite successful authorization
