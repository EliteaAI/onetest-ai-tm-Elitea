---
id: ELITEA-3502
title: "Required-Field Validation Blocks Credential Creation"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3502: Required-Field Validation Blocks Credential Creation

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify a credential cannot be tested/saved while required fields (Client ID, Client Secret, OAuth Discovery Endpoint) are missing, since "Test Connection" is gated by `enabled_when.all_fields_set`.

## Preconditions

- Logged in to `{{base_url}}` with permission to create credentials

## Test Data

- Client ID: `test-client-id`
- Client Secret: `test-client-secret`
- OAuth Discovery Endpoint: `https://login.microsoftonline.com/{tenant_id}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Outlook credential form and leave Client ID, Client Secret, and OAuth Discovery Endpoint empty | "Test Connection" button is disabled |
| 2 | Fill in only Client ID | "Test Connection" remains disabled |
| 3 | Fill in Client Secret and OAuth Discovery Endpoint as well (all three required fields set) | "Test Connection" becomes enabled |

## Expected Final State

"Test Connection" is enabled only once all required fields are populated; no credential has been saved yet.

## Pass/Fail Criteria

**Pass:**
- "Test Connection" stays disabled while any required field is empty
- "Test Connection" becomes enabled once all required fields are filled

**Fail:**
- "Test Connection" is enabled with required fields missing
- Credential can be saved without required fields
