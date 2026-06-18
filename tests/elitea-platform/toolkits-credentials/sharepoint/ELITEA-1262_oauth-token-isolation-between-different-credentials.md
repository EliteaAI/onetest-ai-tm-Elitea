---
id: ELITEA-1262
title: "OAuth Token Isolation Between Different Credentials"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2438]
---
# ELITEA-1262: OAuth Token Isolation Between Different Credentials

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that OAuth tokens obtained for one SharePoint credential are not shared with or applied to a different SharePoint credential, even if both are Delegated mode.

**Coverage:**
- Credential A has token for tenant-A.microsoftonline.com
- Credential B has no token or has token for different tenant
- Running a tool with Credential A toolkit does NOT use Credential B token
- Token lookup key is the oauth_discovery_endpoint, ensuring per-credential isolation

## Preconditions

- Two Delegated-mode SharePoint credentials exist:
  - sp-delegated-tenant-A: with token from `https://login.microsoftonline.com/<tenant-A-id>`
  - sp-delegated-tenant-B: no token or different tenant
- Two toolkits configured, one per credential

## Test Data

- Credential A endpoint: `https://login.microsoftonline.com/<tenant-A-id>`
- Credential B endpoint: `https://login.microsoftonline.com/<tenant-B-id>` (different tenant or no token)
- Agent A uses toolkit A (Credential A)
- Agent B uses toolkit B (Credential B — no valid token)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login with Credential A via the Login button. Confirm token stored for Tenant A endpoint | Token present in session storage for Credential A endpoint key |
| 2 | DO NOT log in with Credential B | Credential B has no valid token |
| 3 | Open Agent A (uses Credential A toolkit). Send: List files | Tool executes successfully using Credential A token |
| 4 | Open Agent B (uses Credential B toolkit). Send: List files | Tool fails with McpAuthorizationRequired — Credential B has no token. Agent B does NOT use Credential A token |
| 5 | Verify in session storage the tokens are stored under different keys | sessionStorage has separate entries keyed by each credential oauth_discovery_endpoint |

## Expected Final State

sessionStorage has separate entries keyed by each credential oauth_discovery_endpoint

## Pass/Fail Criteria

**Pass:**
- Credential A token is only used by Credential A toolkit
- Credential B toolkit does not fall back to Credential A token
- Token lookup is correctly keyed by oauth_discovery_endpoint
- McpAuthorizationRequired raised for Credential B toolkit without a token

**Fail:**
- Credential B toolkit accidentally uses Credential A token
- Tokens are not isolated between credentials
- Both toolkits work when only one credential has a token
