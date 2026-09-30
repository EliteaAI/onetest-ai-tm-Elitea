---
id: ELITEA-3516
title: "Scopes Field Reflects/Accepts the Delegated Graph Scopes"
priority: medium
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3516: Scopes Field Reflects/Accepts the Delegated Graph Scopes

**Module:** Outlook Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Scopes field in the credential form and the OAuth modal's scope list correctly show `Mail.Read`, `Mail.ReadWrite`, `Mail.Send`, and that `offline_access` is added automatically without requiring the user to type it.

## Preconditions

- N/A

## Test Data

- Scopes: `Mail.Read Mail.ReadWrite Mail.Send`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new Outlook credential form and inspect the Scopes field/default | Field shows/accepts `Mail.Read`, `Mail.ReadWrite`, `Mail.Send` |
| 2 | Open the `McpAuthModal` and inspect the scopes shown for authorization | Same delegated Mail scopes are listed |
| 3 | Inspect the effective scopes sent to Microsoft (e.g. via the consent screen or network request) | `offline_access` appears even though the user did not type it explicitly |

## Expected Final State

The delegated Mail scopes are correctly configured and `offline_access` is always included automatically.

## Pass/Fail Criteria

**Pass:**
- Scopes field and auth modal correctly show the three delegated Mail scopes
- `offline_access` is present in the effective authorization request without manual entry

**Fail:**
- Any of the three Mail scopes is missing from the field or modal
- `offline_access` is absent from the actual authorization request
