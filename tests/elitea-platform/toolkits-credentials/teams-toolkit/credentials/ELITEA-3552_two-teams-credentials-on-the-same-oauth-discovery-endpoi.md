---
id: ELITEA-3552
title: "Two Teams Credentials on the Same OAuth Discovery Endpoint Do Not Share or Leak Tokens"
priority: high
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3552: Two Teams Credentials on the Same OAuth Discovery Endpoint Do Not Share or Leak Tokens

**Module:** Teams Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that when two separate Teams credentials are configured against the same tenant/discovery endpoint, each toolkit instance uses its own token and never picks up the other credential's token.

## Preconditions

- Two distinct Teams credentials exist, both using the same `oauth_discovery_endpoint` (e.g. same tenant, different Azure AD app registrations or different signed-in users)

## Test Data

| Field | Credential 1 | Credential 2 |
|-------|---------------|---------------|
| oauth_discovery_endpoint | same tenant URL | same tenant URL |
| Signed-in user | User A | User B |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Authorize both credentials independently | Each credential has its own distinct access/refresh token stored |
| 2 | Run a Teams tool (e.g. `list_teams`) via Credential 1's toolkit instance | Result reflects User A's teams only |
| 3 | Run the same tool via Credential 2's toolkit instance | Result reflects User B's teams only, with no data or token bleed-through from Credential 1 |

## Expected Final State

Each credential's toolkit instance continues to authenticate exclusively with its own stored token.

## Pass/Fail Criteria

**Pass:**
- Each credential's calls are authenticated with its own token and return only that credential's user's data

**Fail:**
- Either credential's calls are authenticated with, or return data belonging to, the other credential
