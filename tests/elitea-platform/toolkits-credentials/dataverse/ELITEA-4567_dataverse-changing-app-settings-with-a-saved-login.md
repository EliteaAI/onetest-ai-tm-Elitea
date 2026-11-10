---
id: ELITEA-4567
title: "Dataverse — changing URL, tenant, client ID or secret on a credential with a saved login"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8, issue:7491]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7491"]
---

# ELITEA-4567: Dataverse — changing URL, tenant, client ID or secret on a credential with a saved login

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify what happens to a saved login when the credential's app settings change, and that the user can log in again with the new settings.

**Known:** [#7491](https://github.com/EliteaAI/elitea_issues/issues/7491): after the client ID or secret changes, Login shows a client error instead of the Microsoft sign-in.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.
- A second Entra app (or a new secret of the same app).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Edit C: change only the label; save. | Saved; the login stays (`refresh_token` still set); T still shows **Connected!**. |
| 2 | Edit C: set a new client secret of the same app; save. Run who_am_i in AG. | Works with the saved login. |
| 3 | Edit C: set the client ID and secret of the second app; save. | The saved login is removed, or T shows **Not Connected**. |
| 4 | Open T → **Login**. | The Microsoft sign-in opens. (Known bug #7491: "The client secret is wrong or expired." or a similar client error.) |
| 5 | Workaround check: **Logout** on T, then **Login**. | The sign-in opens; after it T shows **Connected!**; who_am_i works. |
| 6 | Edit C: change the URL to another Dataverse environment, then the tenant; save. Run who_am_i. | **Record** whether the old login is kept and what the run returns. |

---

## Expected Final State

C has the original app settings and a fresh login.

---

## Pass/Fail Criteria

**Pass:**
- After a settings change the user can log in again straight from Login.

**Fail:**
- Login shows a client error and never opens the sign-in (#7491).
- A login made for another app or environment is silently used.
