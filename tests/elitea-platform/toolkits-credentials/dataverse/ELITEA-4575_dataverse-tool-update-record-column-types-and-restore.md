---
id: ELITEA-4575
title: "Dataverse tools — update_record: text, number, date, choice, boolean, multi-select, lookup and clear"
priority: critical
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4575: Dataverse tools — update_record: text, number, date, choice, boolean, multi-select, lookup and clear

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Functional

**Objective:** Verify update_record changes each column type of one existing record, as MS-A, and the change is visible in Dataverse.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A test record **R** that MS-A can edit, created for testing (e.g. an Account named `QA-DV test`), with its entity set and GUID noted. Restore or delete it after the test.
- Original values of the columns used, noted before the test.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ask AG: "set the description of <R> to 'QA-DV marker'". | The agent calls describe_entity first, then update_record; "Updated 1 column(s) on <set>(<guid>)". |
| 2 | get_record R. | The new value; Modified By = MS-A in Dataverse. |
| 3 | update_record with a number, a date (ISO 8601), a choice value and a boolean. | Each saved; get_record shows the values and their labels. |
| 4 | Multi-select choice as `"1,2"` (if the table has one). | Saved. |
| 5 | Lookup `{"<nav>@odata.bind": "/accounts(<guid>)"}`. | Saved; the lookup shows the target. |
| 6 | A column set to `null`. | Cleared. |
| 7 | Restore the original values; get_record. | Back to the original values. |

---

## Expected Final State

R has its original values.

---

## Pass/Fail Criteria

**Pass:**
- Every column type is updated and read back.

**Fail:**
- A value is saved wrongly or the update acts as another user.
