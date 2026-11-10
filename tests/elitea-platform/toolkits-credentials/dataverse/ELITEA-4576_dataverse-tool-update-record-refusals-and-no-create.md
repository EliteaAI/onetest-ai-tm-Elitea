---
id: ELITEA-4576
title: "Dataverse tools — update_record refusals: owner and status, limits, bad lookups, unknown record, no create"
priority: critical
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4576: Dataverse tools — update_record refusals: owner and status, limits, bad lookups, unknown record, no create

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Functional

**Objective:** Verify update_record refuses what it must not do: system, owner and status columns, too many fields, bad values, unknown records (never creating one), and records MS-A cannot edit.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A test record **R** that MS-A can edit, created for testing (e.g. an Account named `QA-DV test`), with its entity set and GUID noted. Restore or delete it after the test.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | fields `{}`. | "fields must be a non-empty object of column logical names to new values". |
| 2 | 21 columns. | "At most 20 columns per update". |
| 3 | `ownerid`, `statecode`, `statuscode`, `createdon`, also `OwnerId`. | "'<column>' cannot be updated with this tool". |
| 4 | A list or object value (`[1,2]`, `{"a":1}`). | "'<column>': use a plain value (multi-select choices as '1,2')". |
| 5 | Lookup `_x_value`; lookup key with value `accounts(<guid>)` (no slash) or a non-GUID. | "…is not a column logical name; set lookups as '<navigation>@odata.bind'" / "'<key>' must be '/<entity_set>(<guid>)'…". |
| 6 | An unknown column, a wrong type. | "Dataverse returned HTTP 400: …". |
| 7 | A random GUID in the right table. | "Record not found (updates never create new records)"; **no new record** in Dataverse. |
| 8 | A record MS-A cannot edit (if available). | "Your Dataverse user has no permission for this operation". |
| 9 | Ask AG to create a record, delete a record, change the owner or the status. | The agent can't: no tool for create / delete; owner / status refused. |

---

## Expected Final State

R unchanged; no new records.

---

## Pass/Fail Criteria

**Pass:**
- Every refusal has the message above and nothing changes in Dataverse.

**Fail:**
- A record is created, deleted, or its owner / status changed.
