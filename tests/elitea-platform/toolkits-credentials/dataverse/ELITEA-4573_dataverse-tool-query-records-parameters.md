---
id: ELITEA-4573
title: "Dataverse tools — query_records: filter, select, orderby, top, more_available"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4573: Dataverse tools — query_records: filter, select, orderby, top, more_available

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify every query_records parameter and the result shape.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- At least 3 active records in one table (e.g. Accounts) visible to MS-A.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | entity_set only. | Up to 10 records; `count`; `more_available`. |
| 2 | filter `statecode eq 0`, select `name,statecode`, orderby `createdon desc`, top 3. | At most 3 rows, only those columns, newest first. |
| 3 | top 1 with 2 or more matching rows. | `count` 1, `more_available` true. |
| 4 | top 50; a filter that matches fewer rows than top. | All matches; `more_available` false. |
| 5 | top 0, 51, -5. | **Record**: refused by the schema (1 to 50) or clamped to 1 / 50. |
| 6 | filter `name eqq 'x'`. | "Dataverse returned HTTP 400: <Dataverse message>", short and readable. |
| 7 | filter with no match. | `records: []`, `count: 0`, `more_available: false`. |

---

## Expected Final State

No data changed.

---

## Pass/Fail Criteria

**Pass:**
- Parameters are applied and the result shape is right.

**Fail:**
- `more_available` is wrong, or more than top rows are returned.
