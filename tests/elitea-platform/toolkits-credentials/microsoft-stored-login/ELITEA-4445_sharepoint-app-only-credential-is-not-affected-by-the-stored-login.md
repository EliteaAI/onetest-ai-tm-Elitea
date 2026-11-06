---
id: ELITEA-4445
title: "SharePoint App-only credential is not affected by the credential-page stored login, and switching modes leaves no stale login"
priority: medium
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7345, stored-login, sharepoint, p2]
requirements: ["EliteaAI/elitea_issues#7345"]
---

# ELITEA-4445: SharePoint App-only credential is not affected by the credential-page stored login, and switching modes leaves no stale login

**Module:** toolkits-credentials · **Priority:** Medium (P2) · **Type:** Functional

**Objective:** Verify that a SharePoint **App-only** credential (client ID and secret, no user sign-in) keeps working as before #7345: no Login / Logout, nothing saved, and schedules are not blocked. Also record what happens to a saved login when a Delegated credential is switched to App-only and back, since nothing in the #7345 changes clears `refresh_token` on a mode change.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- An Entra app with SharePoint **application** permissions (for App-only) and delegated permissions + `offline_access` (for Delegated). A SharePoint site.
- A pipeline **SPL** that calls `get_lists` through a SharePoint toolkit.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a SharePoint credential **SA** in **App-only** mode (client ID, secret, site URL). Save. | Saved. The page shows **Test connection** only, no **Login** / **Logout**. |
| 2 | Click **Test connection**. | Succeeds without a Microsoft sign-in window. No "Connected! The login is saved…" toast. GET: no `refresh_token`. |
| 3 | Create a toolkit using SA, add it to SPL, add a schedule. | The risk review shows no "needs a personal sign-in" finding; the schedule is saved. |
| 4 | Let SPL run from the schedule. | Succeeds with app-only access. |
| 5 | Create a SharePoint credential **SD** in **Delegated** mode, log in from the credential page. | Login saved (`refresh_token` set). |
| 6 | Switch SD to **App-only**, keep client ID and secret, Save. | Saved. The page shows no Login / Logout. **Record**: GET — is `refresh_token` still on the credential? |
| 7 | Use SD in a schedule. | Not blocked; runs with app-only access. **Record** whether the old saved login is used anywhere. |
| 8 | Switch SD back to **Delegated**, Save. | **Record**: does the page show **Logout** (old login reused) or **Login** (needs a new sign-in)? If Logout, does a scheduled run work with it? |
| 9 | If a stale `refresh_token` remained, as an **editor** open SD and save an unrelated change. | **Record** the result. A save must not fail with 403 "Only project admins can log in or out on a team credential" because of the stale login. |

---

## Expected Final State

App-only credentials never show Login / Logout and never store a login. A mode switch leaves the credential in a state the page shows correctly.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1–4 behave as before #7345.
- After steps 6 and 8, the page state matches what is stored.

**Fail:**
- An App-only credential shows Login / Logout, stores a login, or is blocked in a schedule.
- After a mode switch the page shows a login that doesn't work, or an editor's save fails because of a stale login (file a bug).
