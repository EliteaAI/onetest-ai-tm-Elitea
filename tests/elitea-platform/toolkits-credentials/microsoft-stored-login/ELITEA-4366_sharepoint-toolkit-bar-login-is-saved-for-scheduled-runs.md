---
id: ELITEA-4366
title: "SharePoint: a login from the toolkit page bar is saved and used by a scheduled run"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7037, issue:7309, stored-login, sharepoint, p1]
requirements: ["EliteaAI/elitea_issues#7037", "EliteaAI/elitea_issues#7309"]
---

# ELITEA-4366: SharePoint: a login from the toolkit page bar is saved and used by a scheduled run

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify the supported way to save a SharePoint login: the login bar on the **SharePoint toolkit page**. The login must be saved on the credential and used by scheduled runs. The schedule must not be blocked as needing a personal sign-in (#7309).

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- A SharePoint credential **SC** (as in ELITEA-4365 step 1) with no saved login, and a SharePoint toolkit **ST** using it.
- A pipeline **SPL** that reads a file from the site through ST.

---

## Test Data

| Variant | Discovery endpoint on SC |
|---|---|
| Plain authority | `https://login.microsoftonline.com/<tenant_id>` |
| Ends in `/v2.0` | `https://login.microsoftonline.com/<tenant_id>/v2.0` |

Run steps 1–6 once per variant. The `/v2.0` variant checks the token URL fix from #7309.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open ST. Check the login bar. | The bar shows **Not Connected** and a **Login** button. |
| 2 | Click **Login** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."** The bar shows **Connected!**. |
| 3 | Check the SC GET response in DevTools. | `data.refresh_token` is a `{{secret.…}}` reference. |
| 4 | Add a schedule to SPL. | The schedule is accepted. It is not blocked as needing a personal sign-in. |
| 5 | Let SPL run from the schedule with the browser closed. | The run reads the file. There is no login prompt and no `404` from the token endpoint. |
| 6 | On ST, click **Logout** and confirm. Run SPL again from a schedule. | Toast **"You have successfully logged out!"** The next scheduled run asks for a login. |

---

## Expected Final State

After step 6, SC has no saved login and SPL asks for a login.

---

## Pass/Fail Criteria

**Pass:**
- Both variants save the login, the schedule is accepted, the scheduled run reads the file, and logout removes the login.

**Fail:**
- The schedule is refused as needing a personal sign-in.
- The `/v2.0` variant fails with a token endpoint error.
