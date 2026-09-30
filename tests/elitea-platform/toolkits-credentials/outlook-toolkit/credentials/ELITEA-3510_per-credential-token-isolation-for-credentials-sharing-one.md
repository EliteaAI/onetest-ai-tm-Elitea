---
id: ELITEA-3510
title: "Per-Credential Token Isolation for Credentials Sharing One Discovery Endpoint"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3510: Per-Credential Token Isolation for Credentials Sharing One Discovery Endpoint

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify two distinct Outlook credentials pointing at the same `oauth_discovery_endpoint` maintain independent tokens, since the storage key is `"<credential_uuid>:<oauth_discovery_endpoint>"`.

## Preconditions

- Two Outlook credentials created, both using the same tenant discovery endpoint but different Client ID/Secret (or the same app, different credential records)

## Test Data

- Credential 1: `outlook-cred-1`
- Credential 2: `outlook-cred-2`
- Shared OAuth Discovery Endpoint: `https://login.microsoftonline.com/{tenant_id}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Authorize Credential 1 | Credential 1 shows logged in |
| 2 | Open Credential 2 | Credential 2 independently shows "Login" (not logged in) despite sharing the discovery endpoint |
| 3 | Authorize Credential 2 | Credential 2 shows logged in |
| 4 | Log out of Credential 1 only | Credential 2 remains logged in and functional (Test Connection still succeeds) |

## Expected Final State

Credential 1 is logged out; Credential 2 remains authorized and independently functional.

## Pass/Fail Criteria

**Pass:**
- Each credential's login state is independent of the other despite the shared discovery endpoint
- Logging out one credential does not affect the other

**Fail:**
- Authorizing/logging out one credential affects the other's token state
