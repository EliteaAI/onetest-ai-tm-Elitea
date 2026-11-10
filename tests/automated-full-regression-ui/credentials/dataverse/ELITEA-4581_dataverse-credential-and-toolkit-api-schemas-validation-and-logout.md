---
id: ELITEA-4581
title: "Dataverse — credential and toolkit API: schemas, vault storage, URL and authority checks, no-login 401, logout"
priority: high
type: regression
module: toolkits-credentials/dataverse
status: draft
execution_type: manual
tags: [automated:API:regression, feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4581: Dataverse — credential and toolkit API: schemas, vault storage, URL and authority checks, no-login 401, logout

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Regression

**Objective:** API regression of the Dataverse credential and toolkit without a Microsoft sign-in. Manual source: ELITEA-4564, 4565, 4569.

---

## Preconditions

- JWT of a project admin of team project **P**.
- Test app values (any tenant GUID and client values work for steps 1 to 6).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | GET the configuration types and toolkit schemas. | Type `dataverse` with url, tenant_id, client_id, client_secret and hidden `refresh_token`; toolkit `dataverse` with who_am_i, get_record, query_records, describe_entity (group read), update_record (group write). |
| 2 | Outlook, Teams, SharePoint schemas. | Each has the hidden write-only `refresh_token`. |
| 3 | POST a Dataverse credential, then PUT with `refresh_token` = a dummy value; GET it and list. | `client_secret` and `refresh_token` are `{{secret.…}}`; values never returned. |
| 4 | Check connection with URL `https://example.com`. | 400 "Dataverse URL must look like https://<org>.crm.dynamics.com". |
| 5 | Outlook credential with `oauth_discovery_endpoint=https://evil.example.com/x`. | 400 "Must be https://login.microsoftonline.com/<tenant_id>". |
| 6 | Dataverse check connection with no `refresh_token`. | 401 `requires_authorization: true`, auth metadata with `https://login.microsoftonline.com/<tenant>`; toolkit validator: "Sign in to Dataverse to connect this credential.". |
| 7 | PUT without `refresh_token` (logout). | 200; `refresh_token` gone; validator back to "Sign in…". |

---

## Expected Final State

Test credentials deleted.

---

## Pass/Fail Criteria

**Pass:**
- All responses as above.

**Fail:**
- A secret value is returned, or a check is not enforced.
