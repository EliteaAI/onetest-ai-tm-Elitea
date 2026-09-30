---
id: ELITEA-3552
title: "Create a Teams Credential End-to-End via Delegated OAuth"
priority: critical
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3552: Create a Teams Credential End-to-End via Delegated OAuth

**Module:** Teams Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify a Teams credential can be created and successfully authorized against a live Microsoft 365 tenant via delegated OAuth.

## Preconditions

- Logged in to `{{base_url}}` with permission to create credentials
- Valid Azure AD `client_id` / `client_secret` with the Teams delegated scopes (`Chat.Read` or `Chat.ReadWrite`, `ChatMessage.Send`, `Chat.Create`, `Team.ReadBasic.All`, `Channel.ReadBasic.All`, `ChannelMessage.Send`, `User.Read`/`User.ReadBasic.All`, `offline_access`)
- A live Microsoft 365 test tenant/account available to complete the OAuth consent

## Test Data

| Field | Value |
|-------|-------|
| Credential type | Teams |
| Client ID | valid Azure AD app client ID |
| Client Secret | valid Azure AD app client secret |
| OAuth Discovery Endpoint | `https://login.microsoftonline.com/{tenant_id}` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials → Create Credential, select "Teams", and supply Client ID, Client Secret, and OAuth Discovery Endpoint | Form accepts the values; the "Test Connection" / sign-in action becomes available |
| 2 | Trigger the delegated OAuth sign-in flow and consent to the requested scopes as the test tenant user | Microsoft sign-in/consent screen completes and redirects back to ELITEA without error |
| 3 | Save the credential and re-open it / run "Test Connection" | Credential is saved with a stored access token and refresh token; the connection test succeeds |

## Expected Final State

A Teams credential exists with a valid, stored access token and refresh token, and its connection test reports success.

## Pass/Fail Criteria

**Pass:**
- OAuth consent completes without error and redirects back to ELITEA
- Credential is saved with both access and refresh tokens stored
- Connection test succeeds

**Fail:**
- OAuth flow fails, hangs, or does not return to ELITEA
- Credential saves without a token, or the connection test fails despite a completed consent
