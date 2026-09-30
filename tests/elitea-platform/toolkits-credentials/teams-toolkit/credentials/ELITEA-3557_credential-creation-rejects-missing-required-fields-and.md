---
id: ELITEA-3557
title: "Credential Creation Rejects Missing Required Fields and Missing OAuth Discovery Endpoint"
priority: high
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3557: Credential Creation Rejects Missing Required Fields and Missing OAuth Discovery Endpoint

**Module:** Teams Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that Teams credential creation is validated: `client_id` and `client_secret` are required, and a missing OAuth discovery endpoint is rejected with the specific message returned by `check_connection`.

## Preconditions

- Logged in to `{{base_url}}` with permission to create credentials

## Test Data

| Variant | client_id | client_secret | OAuth Discovery Endpoint | Expected |
|---|---|---|---|---|
| A | empty | valid | valid | Save blocked with required-field error |
| B | valid | empty | valid | Save blocked with required-field error |
| C | valid | valid | empty | Save/test fails with a message stating the OAuth discovery endpoint is required for Teams |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Attempt to save a Teams credential per Variant A | Form blocks saving with a clear required-field error on Client ID |
| 2 | Attempt to save a Teams credential per Variant B | Form blocks saving with a clear required-field error on Client Secret |
| 3 | Attempt to save/test a Teams credential per Variant C | Connection test fails with a message stating the OAuth discovery endpoint is required for Teams |

## Expected Final State

No credential is persisted for any of the three invalid variants.

## Pass/Fail Criteria

**Pass:**
- All three invalid variants are rejected with the specific, correct validation message

**Fail:**
- Any invalid variant is saved successfully, or fails with a generic/unrelated error message
