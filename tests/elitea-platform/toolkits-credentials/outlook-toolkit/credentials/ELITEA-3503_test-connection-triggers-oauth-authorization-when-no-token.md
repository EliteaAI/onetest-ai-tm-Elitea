---
id: ELITEA-3503
title: "Test Connection Triggers OAuth Authorization When No Token Exists"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3503: Test Connection Triggers OAuth Authorization When No Token Exists

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking "Test Connection" on a brand-new Outlook credential (no stored token) opens the OAuth authorization modal rather than failing silently, and that the popup opens immediately without being blocked.

## Preconditions

- Azure AD app registered with delegated Mail.Read/ReadWrite/Send scopes

## Test Data

- Client ID: valid Azure AD app Client ID
- Client Secret: valid Azure AD app Client Secret
- OAuth Discovery Endpoint: `https://login.microsoftonline.com/{tenant_id}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Fill in a valid Client ID, Client Secret, and OAuth Discovery Endpoint | Fields accepted, "Test Connection" enabled |
| 2 | Click "Test Connection" | `McpAuthModal` opens |
| 3 | Inspect the modal content | Modal does not prompt to re-enter Client ID/Client Secret (already supplied via `provided_settings`) — only scopes and an "Authorize" button are shown |
| 4 | Click "Authorize" | A popup window opens immediately, before any network call, and is not blocked |

## Expected Final State

The OAuth authorization popup is open, waiting for Microsoft sign-in; no token has been stored yet.

## Pass/Fail Criteria

**Pass:**
- `McpAuthModal` opens on Test Connection with no existing token
- Client ID/Secret are not re-requested in the modal
- Popup opens immediately and is not blocked

**Fail:**
- Test Connection fails silently or shows a generic error instead of opening the modal
- Modal re-requests Client ID/Secret
- Popup is delayed until after a network call, or blocked without a fallback message
