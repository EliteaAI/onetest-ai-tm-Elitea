---
id: ELITEA-4444
title: "SharePoint credential-page login and scheduled runs work with both discovery endpoint forms, and the schedule check blocks only what needs a live sign-in"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, int:oauth, int:sharepoint, issue:7345, issue:7309, stored-login, sharepoint, p1]
requirements: ["EliteaAI/elitea_issues#7345", "EliteaAI/elitea_issues#7309"]
---

# ELITEA-4444: SharePoint credential-page login and scheduled runs work with both discovery endpoint forms, and the schedule check blocks only what needs a live sign-in

**Module:** toolkits-credentials · **Priority:** High (P1) · **Type:** Functional

**Objective:** Verify the #7345 acceptance criterion "both discovery endpoint forms work" for a login saved from the **credential page**: the token URL drops a trailing `/v2.0` (elitea-sdk #818, elitea_core #642), so the toolkit page shows Connected with no "requires OAuth" warning and scheduled runs refresh the token. Also verify that the schedule risk review (#7309) blocks a SharePoint toolkit only when no login is saved, and still blocks other toolkits that need a live sign-in.

---

## Preconditions

- A team project **P**. The tester is a **project admin**.
- An Entra app with SharePoint delegated permissions (for example `Sites.Read.All`) and `offline_access`, and a SharePoint site the test account **MS-A** can read.
- A pipeline **SPL** with one node that calls `get_lists` (or reads a file) through a SharePoint toolkit.
- For step 9: an OpenAPI or remote MCP toolkit that needs a live OAuth sign-in.

---

## Test Data

| Variant | Discovery endpoint on the SharePoint credential |
|---------|-------------------------------------------------|
| Tenant | `https://login.microsoftonline.com/<tenant_id>` |
| `/v2.0` | `https://login.microsoftonline.com/<tenant_id>/v2.0` |
| `/v2.0/` | `https://login.microsoftonline.com/<tenant_id>/v2.0/` |

Run steps 1–6 once per variant, each with a new credential **SC** and toolkit **ST**.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create SC (Delegated) with the variant's endpoint, save, and create ST using it. Add ST to SPL and try to add a schedule. | The risk review shows the blocking finding **"Toolkit needs a personal sign-in"** (no login saved yet). |
| 2 | On SC's **credential page**, click **Test connection** and sign in as MS-A. | Toast **"Connected! The login is saved for scheduled runs."**; GET shows `data.refresh_token` as a `{{secret.…}}` reference. |
| 3 | Open ST. | **One** login bar (SharePoint's own), showing **Connected!**. No "requires OAuth" warning next to it. |
| 4 | Add the schedule to SPL again. | No blocking finding; the schedule is saved. |
| 5 | Let SPL run from the schedule with the browser closed, at least once after 1 hour (so the token is refreshed, not read from the cache). | Runs succeed and return the site's lists. The run log has no 404 from `…/v2.0/oauth2/v2.0/token`. |
| 6 | Ask an agent with ST in chat, from a browser with no Microsoft sign-in. | The tool runs with the saved login, no login prompt. |
| 7 | **Record:** on the `/v2.0` SC, change the endpoint to the tenant form (no `/v2.0`) and save. Reload SC and ST. | Note whether the page still shows Logout / Connected and whether a scheduled run still works without a new login. (The browser token key includes the endpoint text; the saved login does not.) |
| 8 | Repeat steps 2–5 with an **Outlook** and a **Teams** credential on the `/v2.0` form. | Toolkit page shows Connected with no "requires OAuth"; scheduled runs succeed (same SDK fix). |
| 9 | In the same pipeline, add the OpenAPI / MCP toolkit that needs a live sign-in, and try to schedule. | Still blocked with "Toolkit needs a personal sign-in" for that toolkit only. |
| 10 | Compare the blocking result shown in the schedule dialog (UI) with the saved schedule (backend) for steps 1, 4 and 9. | Both agree in every step. |

---

## Expected Final State

Every variant has a saved login, its schedule is accepted, and scheduled runs succeed. Toolkits that still need a live sign-in stay blocked.

---

## Pass/Fail Criteria

**Pass:**
- All three endpoint forms save the login from the credential page, show Connected without a warning, and refresh in scheduled runs.
- The risk review blocks SharePoint only without a saved login, and still blocks OpenAPI / MCP.

**Fail:**
- A `/v2.0` variant shows "requires OAuth" next to Connected, or a scheduled run fails with a token endpoint 404.
- A schedule with a saved SharePoint login is blocked, or a toolkit that needs a live sign-in is not.
- The UI and backend schedule checks disagree.
