---
id: ELITEA-4572
title: "Dataverse tools — who_am_i and get_record: output and parameters"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4572: Dataverse tools — who_am_i and get_record: output and parameters

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify who_am_i and every get_record parameter (entity_set, record_id, select) with valid and invalid values.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A test record **R** that MS-A can edit, created for testing (e.g. an Account named `QA-DV test`), with its entity set and GUID noted. Restore or delete it after the test.
- Run the tools from the agent chat or the toolkit **Test settings**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | who_am_i. | UserId, BusinessUnitId, OrganizationId; no `@odata` keys; UserId = MS-A. |
| 2 | get_record entity_set `systemusers`, record_id = UserId, select `fullname,internalemailaddress`. | Only those columns plus the id; MS-A's name. |
| 3 | get_record on R with no select. | All columns; choice / lookup columns have `…@OData.Community.Display.V1.FormattedValue`; lookups as `_<name>_value`. |
| 4 | record_id in braces `{<guid>}` and with spaces; select `name, statecode`. | Accepted. |
| 5 | record_id `123`. | "record_id must be a GUID". |
| 6 | entity_set `accounts?$top=1`, `../x`, empty. | "entity_set must be a Dataverse entity set name, e.g. 'opportunities' or 'accounts'". |
| 7 | select `name;drop`, `name,`. | "select must be a comma-separated list of column logical names". |
| 8 | Unknown entity set; a random GUID. | "Record or table not found". |
| 9 | A record MS-A cannot read (if available). | "Your Dataverse user has no permission for this operation". |

---

## Expected Final State

No data changed.

---

## Pass/Fail Criteria

**Pass:**
- Valid calls return data; invalid values return the messages above.

**Fail:**
- An invalid value reaches Dataverse or returns a raw error.
