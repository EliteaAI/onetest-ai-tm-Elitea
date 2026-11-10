---
id: ELITEA-4574
title: "Dataverse tools — describe_entity: columns, search, choice values, lookup bind targets"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4574: Dataverse tools — describe_entity: columns, search, choice values, lookup bind targets

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify describe_entity lists only updatable columns, and with search returns choice values and lookup bind keys.

**Known:** The tool description uses OneCRM table names as examples (`epam_engagements`), which don't exist in other environments (expected error there).

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A table with text, choice, boolean and lookup columns (e.g. accounts).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | entity_set `accounts`, no search. | Columns with name, label, type, required; no system columns (createdon, modifiedon, ownerid, statecode, statuscode); note "Option values are omitted here; call again with search to get them."; `how_to_set` hints. |
| 2 | search `name` (any case). | Only columns whose name or label matches. |
| 3 | search a choice column (e.g. `industry`). | The column with `options` (value + label). |
| 4 | search a boolean column. | Options false / true with labels. |
| 5 | search a lookup (e.g. `primary contact`). | `bind_targets` with key `<nav>@odata.bind` and `value_format` `/<entity_set>(<guid>)`. |
| 6 | Unknown entity set (e.g. `epam_engagements` outside OneCRM). | "No table with entity set '<x>'". |
| 7 | A big table with no search. | At most 150 columns; `total_matching` gives the real count. |

---

## Expected Final State

No data changed.

---

## Pass/Fail Criteria

**Pass:**
- The output is enough to build an update_record call.

**Fail:**
- System columns are listed, or options / bind targets are missing with search.
