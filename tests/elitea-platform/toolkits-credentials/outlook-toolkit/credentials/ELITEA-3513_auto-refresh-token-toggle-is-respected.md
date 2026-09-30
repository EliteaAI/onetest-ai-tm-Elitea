---
id: ELITEA-3513
title: "Auto-Refresh Token Toggle Is Respected"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3513: Auto-Refresh Token Toggle Is Respected

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify the `auto_refresh_token` setting (default `True`) controls whether an expired token is silently refreshed.

## Preconditions

- Ability to force/wait for access-token expiry

## Test Data

- Credential A: `auto_refresh_token = False`
- Credential B: `auto_refresh_token = True`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create Credential A with `auto_refresh_token` explicitly `False` and authorize it | Credential A is authorized |
| 2 | Let/force Credential A's access token to expire | Token is expired |
| 3 | Trigger Test Connection on Credential A | Connection does not silently refresh; manual re-authorization is required |
| 4 | Repeat steps 1–3 with Credential B (`auto_refresh_token = True`) using an expired-but-refreshable token | Token is refreshed transparently without prompting the user; Test Connection succeeds |

## Expected Final State

Credential A requires manual re-authorization after expiry; Credential B remains functional via silent refresh.

## Pass/Fail Criteria

**Pass:**
- `auto_refresh_token = False` blocks silent refresh
- `auto_refresh_token = True` performs silent refresh transparently

**Fail:**
- A `False` credential is silently refreshed anyway
- A `True` credential still prompts for manual re-authorization when refresh should have succeeded
