---
id: ELITEA-3508
title: "Client Secret Is Never Exposed in Plaintext"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3508: Client Secret Is Never Exposed in Plaintext

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Client Secret is masked everywhere it could surface — form field, saved-credentials list, error messages, and network responses.

## Preconditions

- Access to browser dev tools / network tab

## Test Data

- Client Secret: `super-secret-value-12345`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enter a Client Secret and save/test the credential | Credential is saved/tested |
| 2 | Inspect the Client Secret field in the UI | Field is masked (password-style) |
| 3 | Trigger each error path: missing discovery endpoint (ELITEA-3505), 401 (ELITEA-3506), 403 (ELITEA-3507), and a network timeout (ELITEA-3512) | None of the returned messages contain the raw secret value |
| 4 | Inspect the API response for the credential via the network tab | `client_secret` is not returned in plaintext |

## Expected Final State

The Client Secret is never observable in plaintext in the UI, error messages, or API responses.

## Pass/Fail Criteria

**Pass:**
- Secret is masked in the form
- No error message or API response leaks the raw secret

**Fail:**
- Secret appears unmasked anywhere, in any error message, or in a network response
