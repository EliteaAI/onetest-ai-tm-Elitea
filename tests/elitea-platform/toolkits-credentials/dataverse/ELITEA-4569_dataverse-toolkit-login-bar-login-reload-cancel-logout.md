---
id: ELITEA-4569
title: "Dataverse toolkit page — Login bar: login, reload, cancel, logout"
priority: critical
type: functional
module: toolkits-credentials/dataverse
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, int:dataverse, issue:7037, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7037"]
---

# ELITEA-4569: Dataverse toolkit page — Login bar: login, reload, cancel, logout

**Module:** toolkits-credentials/dataverse · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Login / Logout bar on the Dataverse toolkit page: login saves the login on the credential, the state survives a reload, cancel changes nothing, logout removes the saved login.

---

## Preconditions

- **Dataverse test setup** (see #7037): a Dataverse environment `https://<org>.crm<N>.dynamics.com`; an Entra app (Web platform, redirect URI `https://<elitea-host>/app/mcp-auth-callback`, client secret) with the **delegated** permissions Dynamics CRM `user_impersonation` and `offline_access`, consent granted; a Microsoft account **MS-A** with a Dataverse security role that can read and edit test records.
- A Dataverse (OneCRM) credential **C** (URL, Tenant ID, Client ID, Client secret of the test app) in team project **P**. No login saved. Tester is project admin.
- A Dataverse toolkit **T** using C, all tools selected, and an agent **AG** with T.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open T. | Bar **Not Connected** + **Login**. |
| 2 | **Login** → sign-in dialog → **Cancel**. | Nothing saved; bar still Not Connected. |
| 3 | **Login** → **Authorize** → close the Microsoft window without signing in. | Nothing saved; clear message or no change. |
| 4 | **Login** → sign in as MS-A (the account picker lets you choose an account). | Toast "Connected! The login is saved for scheduled runs."; bar **Connected!** + **Logout**; C has `refresh_token`. |
| 5 | Reload the page; open T in another browser. | **Connected!** in both (the login is on the server, not in the browser). |
| 6 | **Logout** → dialog → **Cancel**. | Still connected. |
| 7 | **Logout** → **Log out**. | "You have successfully logged out!"; bar **Not Connected**; `refresh_token` removed from C. |

---

## Expected Final State

C has no saved login (log in again for other cases).

---

## Pass/Fail Criteria

**Pass:**
- Login, reload and logout behave as above.

**Fail:**
- A login is not saved, or a logout leaves `refresh_token` on C.
