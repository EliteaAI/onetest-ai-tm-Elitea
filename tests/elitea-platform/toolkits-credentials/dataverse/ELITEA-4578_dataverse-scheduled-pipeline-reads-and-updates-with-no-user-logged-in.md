---
id: ELITEA-4578
title: "Dataverse — scheduled pipeline reads and updates a record with no user logged in (acceptance)"
priority: critical
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4578: Dataverse — scheduled pipeline reads and updates a record with no user logged in (acceptance)

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the main goal of #7037: a scheduled pipeline uses the saved Dataverse login with no browser session, reads a record and updates a field, also in long and parallel runs.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A test record **R** that MS-A can edit, created for testing (e.g. an Account named `QA-DV test`), with its entity set and GUID noted. Restore or delete it after the test.
- A pipeline **PL**: toolkit node get_record (R, select `name,description`) → toolkit node update_record (description = `QA-DV scheduled <date>`) → LLM node summarising.
- Optional: update_record listed in Admin Portal → Guardrails → Sensitive Action Tools.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a schedule for PL (every 5 min or a time in 10 min), approval rule **Run without asking**. Log out of ELITEA and close all browsers. | — |
| 2 | After the run, log in and open the schedule's **Runs**. | Run **Success**: get_record returned R, update_record "Updated 1 column(s)…". |
| 3 | Check R in Dataverse. | Description = the new value; Modified By = MS-A. |
| 4 | If update_record is a sensitive tool: approval rule **Pause and ask me**, next run. | The run waits before update_record; Approve → updated; Reject → no change. |
| 5 | Two schedules on PL at the same minute. | Both succeed (no false "not logged in"). |
| 6 | A run longer than 1 hour (e.g. a wait or many calls), if possible. | The access token is refreshed on 401 and the run continues. |
| 7 | Logout on T; wait for the next run. | The run reports that a login is needed; no update. |
| 8 | Log in on T as MS-B; next run. | Runs as MS-B (who_am_i or Modified By). |

---

## Expected Final State

R restored; schedules deleted.

---

## Pass/Fail Criteria

**Pass:**
- Steps 2 and 3 pass with nobody logged in.

**Fail:**
- A scheduled run fails while a valid login is saved.
- A run after logout still uses the old login.
