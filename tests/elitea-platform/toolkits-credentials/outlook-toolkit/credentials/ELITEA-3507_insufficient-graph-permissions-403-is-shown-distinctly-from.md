---
id: ELITEA-3507
title: "Insufficient Graph Permissions (403) Is Shown Distinctly From Expired Token (401)"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3507: Insufficient Graph Permissions (403) Is Shown Distinctly From Expired Token (401)

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify a 403 (token valid but missing Mail permissions) is reported as a plain error and does not trigger the re-authorization modal, since re-authorizing the same under-scoped app would not fix it.

## Preconditions

- A valid, non-expired token whose granted scopes do not include the required Mail scopes (e.g. consent given without Mail.Read)

## Test Data

- Azure AD app/consent configured without Mail Graph permissions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Authorize the credential with an Azure AD app/consent that lacks Mail Graph permissions | Token is stored, but lacks Mail scopes |
| 2 | Click "Test Connection" | Graph returns 403 |
| 3 | Inspect the response | Plain string "Access forbidden - token lacks required Microsoft Graph Mail permissions" is shown as a form error |
| 4 | Observe the UI | No OAuth popup/re-authorization modal is triggered |

## Expected Final State

The credential shows a plain permissions error; no re-authorization prompt is shown since the existing token is still technically valid.

## Pass/Fail Criteria

**Pass:**
- 403 produces the exact documented plain-error message
- No auth modal is triggered for a 403

**Fail:**
- 403 is treated the same as a 401 (triggers re-authorization)
- Error message differs from the documented text
