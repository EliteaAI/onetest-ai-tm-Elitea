---
id: ELITEA-4571
title: "Dataverse — expired or revoked login and a wrong client secret"
priority: high
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4571: Dataverse — expired or revoked login and a wrong client secret

**Module:** toolkits-credentials/dataverse · **Priority:** High · **Type:** Functional

**Objective:** Verify the toolkit page, runs and messages when the saved login is revoked at Microsoft, and when the client secret is wrong.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/mcp/callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.
- A login for MS-A saved on C (toolkit page → **Login**), unless the case says otherwise.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | At Microsoft, revoke MS-A's sessions (Sign out everywhere or password change). Wait 1 hour (cached access token). | — |
| 2 | Open T. | Bar **Not Connected** + Login; message about logging in again ("The Dataverse login expired or was revoked: log in again."), no raw error. |
| 3 | Run who_am_i in AG. | The run asks for a login; no crash, no stack trace. |
| 4 | Log in again on T. | Connected; who_am_i works. |
| 5 | Edit C: set a wrong client secret; save. Open T. | A clear "The client secret is wrong or expired.". **Record** whether the bar wrongly shows **Connected!** next to it. |

---

## Expected Final State

C has the correct secret and a valid login.

---

## Pass/Fail Criteria

**Pass:**
- A dead login is shown as Not Connected and a re-login fixes it.

**Fail:**
- A dead login still shows Connected!
- Runs crash or show raw errors.
