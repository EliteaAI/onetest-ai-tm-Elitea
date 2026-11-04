---
id: ELITEA-4446
title: "SharePoint Default app credential: credential-page login is saved, and an admin app with a /v2.0 endpoint signs in"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7345, issue:7149, stored-login, sharepoint, p1]
requirements: ["EliteaAI/elitea_issues#7345", "EliteaAI/elitea_issues#7149"]
---

# ELITEA-4446: SharePoint Default app credential: credential-page login is saved, and an admin app with a /v2.0 endpoint signs in

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify the SharePoint credential-page login with admin-managed OAuth apps (#7149): a **Default app** credential's login is saved and used by schedules. Also check two suspected issues from the code:
- An admin app saved with a `…/<tenant>/v2.0` endpoint is accepted, but its token URL is built without dropping `/v2.0` (configurations `token_endpoint`), so admin **Test connection** and the Default app sign-in may fail with a 404. The `/v2.0` fixes from #7345 / #7309 were made only in elitea-sdk and elitea_core.
- When a Default app takes over a credential that has a saved login, the credential list no longer returns `refresh_token`, so the **UI** schedule check may disagree with the backend.

---

## Preconditions

- Admin Portal access (platform admin).
- A team project **P** with a project admin **ADM**.
- No other enabled OAuth app. An Entra app (client ID, secret, tenant) with SharePoint delegated permissions + `offline_access`.
- A pipeline **SPL** that calls `get_lists` through a SharePoint toolkit, and a SharePoint site MS-A can read.

---

## Steps

### Part A: Default app, tenant endpoint

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Admin Portal → OAuth Apps, create **APP_T** on Project 1, **Default**, SharePoint on, scopes `Sites.Read.All`, endpoint `https://login.microsoftonline.com/<tenant_id>`. Test connection. | "The client ID and secret are valid". Saved. |
| 2 | As ADM in P, create a SharePoint credential **SC1** (Delegated): no switcher, "Sign-in settings are managed by your administrator." Save with a name and site URL. | Saved with `oauth_app_id`. |
| 3 | On SC1's credential page, click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."**; `refresh_token` stored. |
| 4 | Create a toolkit with SC1, add it to SPL, schedule it, close the browser. | Schedule accepted; the run returns the site's lists. |

### Part B: admin app with a `/v2.0` endpoint (suspected bug)

| # | Action | Expected Result |
|---|--------|-----------------|
| 5 | Edit APP_T: change the endpoint to `https://login.microsoftonline.com/<tenant_id>/v2.0` (Replace the secret, as required). Click **Test connection**. | Expected: "The client ID and secret are valid". **Suspected:** an error from Microsoft (404 on `…/v2.0/oauth2/v2.0/token`). Record the message. |
| 6 | Save APP_T. | **Record** whether Save is accepted. |
| 7 | As ADM, create SharePoint credential **SC2** on the Default app and log in from the credential page. | Expected: login saved. **Suspected:** sign-in fails at the token exchange (proxy error / `app_unavailable` / 404). Record the error. |
| 8 | If step 7 worked, run the schedule with SC2. | Succeeds. |
| 9 | Restore APP_T's endpoint to the tenant form. | Test connection and sign-in work again. |

### Part C: Default app takes over a credential with a saved login

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Set APP_T Default **off**. As ADM, create a **Custom app** SharePoint credential **SC3** (own Entra app), log in from the credential page (login saved), and schedule SPL with it. | Schedule accepted. |
| 11 | Set APP_T Default **on** again. Before SC3 is used, open the schedule dialog for SPL (UI check), then save the schedule. | **Record** what the UI check shows and what the backend accepts. Expected: both agree that the run needs one new sign-in (the old login belongs to the own client). |
| 12 | As ADM, log in on SC3 from the credential page. Run the schedule. | Works with APP_T's client. |

---

## Expected Final State

SC1 and SC3 have logins saved with APP_T's client, and schedules work. APP_T uses the tenant endpoint.

---

## Pass/Fail Criteria

**Pass:**
- Part A: the Default app login is saved from the credential page and used by the schedule.
- Part B: a `/v2.0` admin app endpoint either works, or is rejected on save with a clear message.
- Part C: UI and backend agree.

**Fail:**
- Part B: the `/v2.0` endpoint is accepted on save but Test connection or sign-in then fails (file a bug: configurations `token_endpoint` needs the same `/v2.0` trim).
- Part C: the UI shows the schedule as fine while the run fails, or blocks a schedule the backend accepts.
